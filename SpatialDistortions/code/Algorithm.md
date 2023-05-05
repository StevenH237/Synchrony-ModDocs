This doc is being written half a year after I actually wrote the algorithm, so it's "coming back Nix's" interpretation of it. But this is the algorithm for how the floors are shuffled! Headers are organized by which function starts first (we're starting with the `Event.levelSequenceUpdate.add` line, and each header is a sub-function it spins off, sub-headers being sub-functions under that, etc etc).

# The main routine
The first check we run is for the current game mode. We want to only run in a few game modes. Right now it's set to only the modes with the IDs `AllZones`, `AllZonesSeeded`, `SingleZone`, or `CustomDungeon`. This seems to include multi-char variants of those modes, however. But it won't run in Versus or Training, for example. If the mode doesn't match a whitelisted mode, then stop.

# Let's copy some info now.
We'll initiate the `levelDeck` variable to a copy of `ev.sequence`. It'll contain some number of elements that look similar to this:
```lua
{
  boss = 4, -- Not present on non-boss floors
  depth = 1,
  floor = 4,
  type = "Boss", -- or "Necro" for regular floors
  zone = 1
}
```

We'll also initiate the `randomState` variable to a copy of `ev.rng`. It'll look something like this:
```lua
{
  random = {
    state1 = 1895920568,
    state2 = 1365020366,
    state3 = 1964837497
  }
}
```

# Should we have only one (1) final boss?
The `shouldSelectOneFinalBoss()` function checks various settings. If any of the following conditions are true, we'll have just one final boss, so that all the zones are the same length:

* The "Force single final boss" option is selected
* The "Zone order" option isn't set to "Random"
* The "Clustering" option is set to "Level"
* The "Clustering" option is set to "Zone", with the "Preserve boss alignment" option enabled

# Alright, then let's have only one (1) final boss.
The `selectOneFinalBoss(levelDeck, randomState)` function actually does that.

It does make a few assumptions, a couple of which might cause unexpected behavior if they're not true:

* There are at least two depths in the dungeon
* All depths except for the final are consistent in length
* The final depth is longer than the rest
* All the floors within each depth are numbered consecutively, 1 to n.

Assuming these are all true, we then have to figure out several things. Our example will use a co-op run between Cadence and Nocturna, which ends with four final bosses and a total of 23 floors.

* `length` is the length of the entire dungeon, simply the number of levels in the level deck. For example, 23.
* `last` is the last level of the dungeon. That's the final item in the level deck. For example, it's the one referencing 5-7.
* `floorsInFinal` is the number of floors in the final depth — simply the floor number of the last level, which is 7 in our example.
* `semifinal` is the last level of the semifinal zone. It's the level in the position of the last level minus that level's own floor count. In our example, that's 23 minus 7, so this would be the 16th level (4-4).
* `floorsInSemifinal`, the floor of the last level of the semifinal zone, is just `semifinal`'s floor number. That'd be 4 in our example.
* `lastGuaranteed` represents the last guaranteed level number. That's the length of the dungeon, minus the length of the final zone, plus the length of the semifinal zone, minus 1. In our example, that'd be 23 minus 7 plus 4 minus 1, or 19.
* `lengthInQuestion` is the length of the dungeon after the last guaranteed level. In our case, 23 minus 19, which is 4.

With all that calculated, now that we know how many floors we're picking between, we have to actually pick one. One is picked at random, and the level from that position is put into the position after `lastGuaranteed` (which is then incremented, in this example to 20, as the selected level is now guaranteed).

So long as the dungeon is longer than the guaranteed level, extra levels should be deleted from the end.

And lastly, we should make the last floor's floor number actually be right (4 in our example).

# What's a "boss alignment"?
Boss alignment is just a record of which floors are boss floors. If we're concerning ourselves with it (baeed on the option), then the `getBossAlignment` function will check whether each floor in the existing sequence and note whether or not there's a boss in that position, then the list of booleans will be returned.

If we're not concerning ourselves with it, an empty list is returned instead.

# The level grid
The `createLevelGrid` function creates a list-of-lists of levels that exist. In the returned `levelGrid`, each object `levelGrid[d][f]` has the following properties:

```lua
{
  depth = d, -- The depth of that level
  floor = f, -- The floor of that level
  exists = true, -- Whether or not the level exists. (Do we need this?)
  prereq = {}, -- The levels that must be placed before this one. We'll cover that in the next couple functions.
  original = i, -- The position of this level within the original arrangement. (Not sure it actually gets used either but...)
  placed = false -- Whether or not this level has been placed in the new sequence yet.
}
```

# Order enforcement (Floor)
The `getFloorOrdering` function sets prerequisites within each zone:

* It quits if the order is random.
* If it's forward, then for each floor `f` except the last, the next floor (`f+1`)'s prerequisite is set to the current floor (`f`) in the same depth, i.e. 2-3 requires 2-2 when evaluating 2-2.
* If it's reverse, then for each floor `f` except the last, that floor (`f`)'s prerequisite is set to the next floor (`f+1`) in the same depth, i.e. 2-2 requires 2-3 when evaluating 2-2.

# Order enforcement (Depth)
The `getZoneOrdering` function sets prerequisits across zones.

Note that it quits immediately if the order is random, but otherwise, for each depth `d` except the last, for each floor that both the current (`d`) and next (`d+1`) depths have in common:

* If the order is forward, the next depth's level (on this floor)'s prerequisite is set to the current depth's level on this floor, i.e. 3-2 requires 2-2 when evaluating depth 2.
* If it's reverse, this depth's level's prerequisite is set to the next depth's level on this floor, i.e. 2-2 requires 3-2 when evaluating depth 2.

# Shuffle levels
Finally, with all that setup aside, it's time to get to the actual meat of the issue, the actual rearrangement of levels. I'm talking about the `shuffleLevels` function - which, of course, has some subroutines of its own.

First, we'll make a new copy of the level deck to draw from, just so that we're not modifying an input. We'll also define a sub-deck, but leave it empty.

> ## The main loop
> This loop will run repeatedly so long as either the main level deck or the sub-deck is non-empty. If the sub-deck has any levels in it, then the rest of the loop will operate just on that. Otherwise, it'll operate on the main deck. In either case, we'll just call it "the deck".
>
> Starting off the loop, we should shuffle the deck. We'll also establish a couple variables to track the last level drawn from the deck and its index, as well as the last drawn *aligned* level and *its* index. The `alignToBoss` variable will track whether this floor *should* be a boss or not.
>
> After that, we'll look through all the levels in the deck in its new shuffled order in...
>
>> ### The deck loop
>> Draw a level from the deck. Don't remove it, just reference it. If its boss (or lack thereof) matches the current floor's alignment correctly, also set it as the aligned draw for the floor.
>>
>> Next, sput off a small function that checks if we can place the drawn level here. This function will return `false` if either (there's a boss alignment and the drawn level doesn't match it) or (the level's prerequisites haven't been satisfied). However, if that returns true, exit this loop.
>>
>> Lastly, if we're already on the final level in the draw deck, but there's an aligned draw, revert the most recent draw to the aligned draw before exiting the loop.
>
> Now that we have a level selected, we need to place it at the end of the sequence and remove it from the deck, as well as marking it as placed for the purposes of prerequisites. Additionally, if we weren't using a sub-deck, we should split the level deck into a main deck and a sub-deck with...
>
>> ### Split the decks
>> This final function in our algorithm first creates a copy of the level deck (again, not modifying inputs) and checks the clustering section. If there's no clustering, there's no splitting.
>>
>> The cluster key should be set to "depth" or "floor" as appropriate. The cluster value is then whatever the value was for that key in the drawn level.
>>
>> For each level remaining in the deck, put it in the sub-deck iff that level's cluster key matches the cluster value; leave it in the main deck otherwise.

After we've finally finished up that function and decided our order, set it in the sequence and let the run begin!