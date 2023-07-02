This is a simple guide to the options of Switcheroo.

**Please [click here](Switcheroo/Options.md) if you have "Show advanced settings" turned off!**

# Replacement Chances
These settings control the chances that items might be replaced, given, or removed.

* **Empty slot fill chance**: The chance that an empty slot (one that doesn't already has an item) gains an item upon randomization.
* **Minimum empty slots**: This controls the number of empty slots that must always be selected (if that many exist) each randomization. Note that if you specify a minimum, that many can be selected even if there's otherwise a 0% chance to select them.
* **Full slot selection chance**: The chance that a filled slot (one that already has an item) is selected to lose or change its item upon randomization.
* **Minimum full slots**: Same as above, except for filled slots.
* **Minimum total slots**: This controls how many total slots must be selected, empty and filled, if their individual minimums don't already satisfy it. Unlike the two previous options, this one can't override a 0% selection chance.
* **Maximum slots**: The maximum number of slots that may be selected on each randomization. Notably, individual and combined minimums override this if they're greater.
* **Selected slot replacement chance**: When a filled slot is selected, this controls the chance that it'll actually receive a new item. If it doesn't, the slot will just be emptied instead. It doesn't apply to empty slots receiving items.
* **Minimum items given**: This is how many items must be given by the mod (if that many slots are selected to receive items). If filled slots are selected, the chance to replace or remove items may be ignored to satisfy this requirement.
* **Maximum items given**: This is how many items may be maximally given by the mod. If this number is reached, remaining slots will not receive items.

# Allowed Floors
This setting controls what floors the mod can activate on. It has the following presets:

* **All floors**: The mod will activate and randomize your build at the start of every floor.
* **Start of run only**: The mod will only activate when you start the run.
* **First of each zone**: The mod will activate on the first floor of each zone.
  * For custom dungeons, this is considered to be the first floor of the run, plus the floor immediately following any boss.
* **After every boss**: The mod will activate on the floor immediately following any boss.
  * For standard dungeons, this is the first floor of any zone, except the first zone.

You can also press enter on this setting to control it more granularly:

* **1st floor (1-1)** to **20th floor (5-4)**: The mod will activate on those specific floors. 
  * For a standard dungeon, the given depth and floor are used.
  * For a custom dungeon, the given ordinal floor number is used, but only if "Custom dungeons use floor numbers" is enabled below.
  * The "1st floor (1-1)" setting always means the first floor of a standard or custom dungeon, regardless of the "Custom dungeons use floor numbers" setting.
* **Extra story boss**: The mod will activate on 5-5 and beyond in a standard dungeon.
* **Custom dungeons use floor numbers**: If this setting is enabled, a custom dungeon will use the "1st floor (1-1)" to "20th floor (5-4)" settings to control the mod on up to the first twenty floors of a custom dungeon, instead of the extra settings below. If disabled, only the "1st floor (1-1)" setting and the extras below will take effect.
* **Training floors**: This mod will activate on training floors. *Note that this setting may eventually be removed, and the mod always activating on such floors. You can simply turn it off to not use it.*
* **Add extra/custom boss floors**: The mod will activate at the start of boss floors in extra zones or custom dungeons.
* **Add extra post-boss floors**: The mod will activate at the start of a floor immediately following a boss in extra zones or custom dungeons.
* **Add other extra floors**: The mod will activate in extra zones or custom dungeons on floors that are neither boss floors nor the next ones thereafter.

# Sell Items
This setting controls whether or not items taken away by the mod are "sold" (if they have a buying price).

It defaults to 0. The percentage entered is the percentage of the *buying* price the item would be sold for.

For now, this setting affects both items given by the mod and items obtained outside it.

# Honor guaranteed transmutations
This setting controls whether or not transmutation fixed outcomes are honored by the mod.

To be more specific, if a filled slot is selected to be replaced, and it contains an item with a transmutation fixed outcome, should that outcome be given to the player? For example, a Ring of Becoming would turn into a Ring of Wonder on the next floor.

This still counts as the new item being given by the mod.

# Don't give...
These settings restrict what items the mod can give.

* **Magic food**: Any consumable healing item that overheals (e.g. Magic Apple). This does include even such items that aren't technically considered food.
* **Movement amplifiers**: Items that cause leaping of multiple tiles per turn (e.g. Boots of Leaping).
* **Incoming-damage increasers**: Items that cause the player to take amplified damage from hits (e.g. Karate Gi).
* **Gold-related items**: Items that collect currency on movement (e.g. Ring of Gold) or shouldn't be given to poverty characters (e.g. Ring of Courage).
  * This entry has an option, "Allow while holding gold". If enabled, players that are holding gold when the floor starts may be given these items.
* **Vision-reducing items**: Items that reduce the player's field of vision (e.g. Ring of Shadows).
* **Floating items**: Items that cause players to float (e.g. Boots of Levitation). Unlike the others, these are allowed by default; the option is simply there to remove them.
* **Deadly items**: Items that kill the player if they get picked up. (The mod prevents such deaths when giving such items.)
* **Banned items**: Items that the player normally cannot get.
* **Don't give components**: Don't give any items that have any components in this list.
* **Don't give items**: Don't give the specific items that are in this list.

# Don't take...
These settings restrict what items the mod can take away. All of these options have a "Take if given by mod" choice, which means that if the mod gave the item, it can take it away like normal, but if the item came from outside the mod, it is permanent.

* **Potion**, **Lucky Charm**, **Crown of Greed**, and **Ring of Wonder**: The specific named items. This won't work on similar modded items.
* **Items locked to character**: If a character is supposed to keep an item, the mod shouldn't take it away.
* **Don't take items unless given**: The specific items in this list can't be taken by the mod, unless they were given by the mod.
* **Don't take components unless given**: Any item with a component in this list can't be taken by the mod, unless it was given by the mod.
* **Don't take items**: The specific items in this list can never be taken by the mod.
* **Don't take components**: Any item with a component in this list can never be taken by the mod.

# Slot settings
* **Allowed slots**: Within which slots can the mod change items?
* **Unlocked slots**: Within which slots should item bans/cursed slots be ignored?
* **One-time slots**: Within which slots should only the first activation of the mod take effect?

You can press enter on any of those to turn on or off individual slots.

* **Slot capacity**: What's the maximum number of items that should be given per slot (if the slot can hold that many items)?
* **Reduce over cap**: If the slot currently holds more items than the cap, should items be taken away?

# Charms settings
* **Charms algorithm**: This setting controls how it's determined how many charms you get on a floor. As of now, there's only one option, but I have ideas for more so this setting exists for forwards compatibility.

# Defaults
These settings control the default item that should be given in each slot. If the mod takes away an item without replacing it, or for some reason fails to generate any item for a given slot, the item selected here will be used instead.

# Generator types
This is a list of item pools that should be used when using the mod. When generating each item, the pools are polled from the top to the bottom of this list until one successfully results in an item.

**Fallback to unweighted genrator** means that if no item was generated by any item pool, an unweighted pool of all items (including internal items) for that slot should be used instead.
