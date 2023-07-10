Components available in Lola:

# `Lola_descentCollectItems`
Any player with this component will "claim" any items they reveal over the course of a floor, and then will collect those items upon descending the stairs.

This component should not be altered directly, but instead through the [`RevealedItems`](./modules/RevealedItems.md) module.

It contains the following fields:

- `active`, bool, default `true`: Controls whether or not the player will receive items. Set to `false` when that player exits the level by death or any means of descent besides the stairs.
- `randomizer`, entityID: Points to a consistency randomizer, which is usually a `Lola_Randomizer`. This component is unset unless needed.
- `revealedItems`, table, default `{}`: The items that this player has revealed, in the order they've done so.

It is given to `Lola_Lola` only.



# `Lola_forcedLowPercent`
Any player with this component dies upon attempting to break low% rules, such as picking up items or bumping bumpable shrines.

It contains the following fields:

- `active`, bool, default `true`: Controls whether or not the player will die getting items. Set to `false` for the duration of the `Lola_descentCollectItems` item collection handler, then `true` again afterwards.
- `killerName`, const localizable string: The string shown when this component kills the player.
- `allowedItems`, const table, default `{}`: Which item types may bypass this rule (entries are `ItemName = true`), though do not bypass the Low% rule itself if active.

It is given to `Lola_Lola` with the following alteration:
```lua
Lola_Lola.Lola_forcedLowPercent = {
  allowedItems = {
    MiscPotion = true
  }
}
```



# `Lola_holders`
Any item with this component tracks which players have held it on this floor. `Lola_forcedLowPercent` is ignored for any item that has already been held by the player attempting to pick it up. It is reset to only the current holder (if any) at the start of each floor.

It is recommended that the [`ItemHolders`](./modules/ItemHolders.md) module be used to interact with this component rather than direct modification.

It contains the following fields:

- `playerIDs`, table, default `{}`: Indicates whether or not the item was held by the player (entries are `[playerID] = true`).
- `safe`, bool, default `false`: Indicates whether or not the item should be treated as having been held by everyone.

It is given to any entity that has the `itemNegateLowPercent` component.



# `Lola_interactedBy`
A storage with this component tracks who last interacted with it and then marks any items it contains as `revealedBy` the same player when the items are revealed. Non-player interactions do not alter this component.

It contains the following field:

- `playerID`, int, default `0`: The player that last interacted with this entity. `0` means no player has.

It is given to any entity that has the `storage` component.



# `Lola_revealedBy`
An item with this component tracks who revealed it, to be collected as part of the `Lola_descentCollectItems` handler.

This component should not be altered directly, but instead through the [`RevealedItems`](./modules/RevealedItems.md) module.

It contains the following field:

- `playerID`, int, default `0`: The player that has revealed the item and claimed it. `0` means no player has.

It is given to any entity with the `itemNegateLowPercent` component.



# `Lola_spellcastPackageItems`
A spellcast marker component that causes the effect of the spellcast to be the packaging of items into crates.

It contains no fields and is given only to `Lola_SpellcastPackage`.



# `Lola_spellcastPackageItemsGreater`
A spellcast marker component that causes the effect of the spellcast to be the packaging of items into chests or (with the proper setting enabled) enemies into crates.

It contains no fields and is given only to `Lola_SpellcastGreaterPackage`.



# `Lola_spellcastFlyawayPackage`
A component that indicates what the spellcast should say in various circumstances, based on the targets of the spell.

It contains the following fields:

- `baseText`, const localizable string, default `""`: What the spellcast flyaway should say when none of the other circumstances apply
- `noTargets`, const localizable string, default `""`: What the spellcast flyaway should say when no items (or enemies, if applicable) are targeted by the spell
- `cantAfford`, const localizable string, default `""`: What the spellcast flyaway should say when some targeted items are too expensive to package
- `enemyCrate`, const localizable string, default `""`: What the spellcast flyaway should say when an enemy is crated by the spell
- `offsetY`, const int, default `0`: The amount by which to move the text up or down on the screen. *⚠ Due to an oversight, currently has no effect.*

It is given to multiple entities as follows:
```lua
Lola_SpellcastPackage.Lola_spellcastFlyawayPackage = {
  baseText = "Package",
  noTargets = "Package (empty)",
  cantAfford = "Package (can't afford)"
}
Lola_SpellcastPackageGreater.Lola_spellcastFlyawayPackage = {
  baseText = "Greater Package",
  noTargets = "Greater Package (empty)",
  cantAfford = "Greater Package (can't afford)",
  enemyCrate = "Greater Package (enemy captured)"
}
```
