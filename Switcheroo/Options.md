This is a simple guide to the options of Switcheroo.

**Please [click here](Options-Advanced.md) if you have "Show advanced settings" turned on!**

# Replacement Chances
These settings control the chances that items might be replaced, given, or removed.

* **Empty slot fill chance**: The chance that an empty slot (one that doesn't already has an item) gains an item upon randomization.
* **Full slot selection chance**: The chance that a filled slot (one that already has an item) is selected to lose or change its item upon randomization.

# Allowed Floors
This setting controls what floors the mod can activate on. It has the following presets:

* **All floors**: The mod will activate and randomize your build at the start of every floor.
* **Start of run only**: The mod will only activate when you start the run.
* **First of each zone**: The mod will activate on the first floor of each zone.
  * For custom dungeons, this is considered to be the first floor of the run, plus the floor immediately following any boss.
* **After every boss**: The mod will activate on the floor immediately following any boss.
  * For standard dungeons, this is the first floor of any zone, except the first zone.

If none of these presets is shown, you likely loaded a ruleset that specifies a different set of floors. Opening the dropdown will allow you to switch to a preset, but you'll have to reload the ruleset to get back what it had.

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
* **Rhythm-ignoring items**: Items that allow the player to temporarily ignore the rhythm (e.g. Heart Transplant).
* **Breakable weapons**: Weapons that can break when the player takes damage, leaving the player defenseless and also dropping a shard (e.g. Glass Dagger).
* **Breakable shovels**: Shovels that can break when the player takes damage, leaving the player unable to dig and also dropping a shard (e.g. Glass Shovel).
* **Deadly items**: Items that kill the player if they get picked up. (The mod prevents such deaths when giving such items.)
* **Banned items**: Items that the player normally cannot get.

# Don't take...
These settings restrict what items the mod can take away. All of these options have a "Take if given by mod" choice, which means that if the mod gave the item, it can take it away like normal, but if the item came from outside the mod, it is permanent.

* **Potion**, **Lucky Charm**, **Crown of Greed**, **Ring of Wonder**, and **Crystal Shovel**: The specific named items. This won't work on similar modded items.
* **Items locked to character**: If a character is supposed to keep an item, the mod shouldn't take it away.
