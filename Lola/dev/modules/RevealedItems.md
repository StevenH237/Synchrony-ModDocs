`local RevealedItems = require "Lola.mod.RevealedItems"`

Module used by Lola to track who revealed which items. The revealed items are tracked in two components:
- The `Lola_revealedBy` component on the item allows an item to have only one claimant.
- The `Lola_descentCollectItems` component on the player allows a player to track the order in which items were revealed.

Always using this module ensures these components are edited in lockstep to stay accurate to each other.

---

# `mark(revealer, item)`: integer
- `revealer` (Entity or integer): Either the entity table or the entity ID of the player that revealed the item. **Not a player ID, use `markPID` instead.**
- `item` (Entity or integer): Either the entity table or the entity ID of the revealed item.

Marks that an item has been revealed by a specific player, claiming the item. If another has already claimed it, their claim is released and their player ID returned. Otherwise, `0` is returned.

If the item is already marked by `revealer`, the item is moved to the end of their list, and their player ID returned.

`nil` is returned when the call fails, which can be caused by:
- `revealer` or `item` do not exist
- `item` cannot be claimed (it doesn't have the `Lola_revealedBy` component)
- `revealer` is not a player (it either doesn't have the `controllable` component, or `controllable.playerID` is `0`).

---

# `markPID(revealerPID, item)`: integer
- `revealerPID` (integer): The player ID of the player that revealed the item. **Not an entity ID, use `mark` instead.**
- `item` (Entity or integer): Either the entity table or the entity ID of the revealed item.

Functions the same as `mark`, except that `revealerPID` should be a player ID instead of an entity ID or table.

---

# `unmark(item)`: integer
- `item` (Entity or integer): Either the entity table or the entity ID of the item to unmark.

Unmarks an item as having been revealed by a player, releasing any claim to it.

Returns the player ID of the player that had claimed it, or `0` if no player had.

`nil` is returned when the call fails, which can be caused by:
- `item` does not exist
- `item` cannot be claimed (it doesn't have the `Lola_revealedBy` component)

---

# `getRevealedItems(player)`: Entity\[\]
- `player` (Entity or integer): Either the entity table or the entity ID of the player whose list to retrieve.

Returns a list of the items revealed by the specified player.

If the player has claimed no items, an empty list is returned.

`nil` is returned when the call fails, which can be caused by:
- `player` does not exist
- `player` cannot claim items (it doesn't have the `Lola_descentCollectItems` component)

---

# `getRevealedItemsPID(playerID)`: Entity\[\]
- `playerID` (integer): The player ID of the player whose list to retrieve.

Functions the same as `getRevealedItems`, except that `playerID` should be a player ID instead of an entity ID or table.