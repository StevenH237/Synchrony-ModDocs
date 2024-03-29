`local ItemHolders = require "Lola.mod.ItemHolders"`

Module used by Lola to track who's already held items. They're tracked in just one component:
- The `Lola_holders` component tracks who's held it.

This module provides convenience methods for editing this component but editing it directly should be safe.

---

# `add(holder, item)`: boolean
- `holder` (Entity or integer): Either the entity table or the entity ID of the player that held the item. **Not a player ID, use `addPID` instead.**
- `item` (Entity or integer): Either the entity table or the entity ID of the held item.

Marks an item as being held by a specific player.

Returns `true` iff the player was added to the list, or `false` if they were already on it (and thus the list has not changed).

`nil` is returned if the call fails, which can be caused by:
- `holder` or `item` do not exist.
- `item` doesn't track holders (it doesn't have the `Lola_holders` component).
- `holder` is not a player (it either doesn't have the `controllable` component, or `controllable.playerID` is `0`).

---

# `addPID(holderPID, item)`: boolean
- `holderPID` (integer): The player ID of the player that held the item. **Not an entity ID, use `add` instead.**
- `item` (Entity or integer): Either the entity table or the entity ID of the held item.

Functions the same as `add`, except that `holderPID` should be a player ID instead of an entity ID or table.

---

# `markSafe(item)`: boolean
- `item` (Entity or integer): Either the entity table or the entity ID of the item to mark safe.

⚠ This function will be implemented in the version after 1.1.5.

Marks an item as safe-for-all, as if it were held by all players. Returns `true` if the change was made successfully, and `false` if nothing changed.

`nil` is returned when the call fails, which can be caused by:
- `item` does not exist.
- `item` doesn't track holders (it doesn't have the `Lola_holders` component).

---

# `reset(item)`: table{integer=boolean}
- `item` (Entity or integer): Either the entity table or the entity ID of the held item.

Resets the list of holders on an item, clearing it except for the current holder (if any). Also clears any safe-for-all mark.

Returns the previous list of holders, in the format `{[playerID] = true}`.

`nil` is returned when the call fails, which can be caused by:
- `item` does not exist.
- `item` doesn't track holders (it doesn't have the `Lola_holders` component).

---

# `check(item, player)`: boolean
- `item` (Entity or integer): Either the entity table or the entity ID of the item to check.
- `player` (Entity or integer): Either the entity table or the entity ID of the player to check against.

Checks whether the given player has held the given item, or the item is marked safe-for-all.

Returns `true` if they have or it is, and `false` otherwise.

`nil` is returned when the call fails, which can be caused by:
- `item` or `player` do not exist.
- `item` doesn't track holders (it doesn't have the `Lola_holders` component).
- `player` isn't a player (it either doesn't have the `controllable` component, or `controllable.playerID` is `0`).

---

# `checkPID(item, playerID)`: boolean
- `item` (Entity or integer): Either the entity table or the entity ID of the item to check.
- `playerID` (integer): The player ID of the player to check against.

Functions the same as `check`, except that `playerID` should be a player ID instead of an entity ID or table.

Notably, the call does not fail if an invalid `playerID` is specified, and will still return `true` for items marked safe-for-all.

---

# `checkAllPIDs(item, playerIDs)`: boolean
- `item` (Entity or integer): Either the entity table or the entity ID of the item to check.
- `playerIDs` (integer\[\]): A list of player IDs to check against.

Checks whether any of the given players have held the given item, or if the item is marked safe-for-all.

Returns `true` if any have or it is, and `false` otherwise.

`nil` is returned when the call fails, which can be caused by:
- `item` does not exist
- `item` doesn't track holders (it doesn't have the `Lola_holders` component).