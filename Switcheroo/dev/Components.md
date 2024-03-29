Components available in Switcheroo:

# `Swticheroo_itemPoolSwitcheroo`
A custom item pool.

This component contains the following fields:

* `weights`, constant table, default `{1}`. This is an item pool component and its `weights` field works the same way.

It's hardcoded to entities as follows:

* Any entity with the `itemPoolSecret` component: Copy the weights from that item pool.
* Any entity *without* the `itemPoolSecret` component, but with the `itemSlot` component (name = `"shield"`) and the `itemPoolBlackChest` component: Copy the weights from that item pool. *Note: There may not be any such entities any more.*



# `Switcheroo_noGive`
Items with this component are not given by the randomizer.

There are no fields or constants on this component.

It is not hardcoded to any entities. However, it is automatically assigned to or removed from items during an entity schema regeneration, depending on player-selected settings. The mod's default settings assign it to:

* Any entity with the `consumableIgnoreRhythmTemporarily` component.
* Any entity with the `itemIncomingDamageIncrease` component.
* Any entity with the `itemIncomingDamageMultiplier` component.
* Any entity with the `itemMoveAmplifier` component.
* Any entity with the `consumableHeal` component where `overheal = true`.
* Any entity with the `itemConsumeOnIncomingDamage` component *and* either the `shovel` or `weapon` components.



# `Switcheroo_noGiveIfBroke`
Items with this component are not given by the randomizer, iff the player has no gold.

It is not hardcoded to any entities. However, it is automatically assigned to or removed from items during an entity schema regeneration, depending on player-selected settings. The mod's default settings assign it to:

* Any entity with the `itemBanPoverty` component.
* Any entity with the `itemBanKillPoverty` component.
* The entities `RingGold` and `RingGoldUncertain`.



# `Switcheroo_noTake`
Items with this component are not taken by the randomizer.

This component contains the following fields:

* `unlessGiven`: constant boolean, default `false`. If it's `true`, items with this component can be taken by the randomizer iff they were given by it.
* `wasGiven`: boolean, default `false`. If it's `true`, the item was given by the randomizer mod, and (if `unlessGiven` is true) can be taken too.

This component isn't hardcoded to any entities. However, it is automatically assigned to or removed from items during an entity schema regeneration, depending on player-selected settings. The mod's default settings assign it to:

* The `CharmLuck` entity: `{ unlessGiven = true }`
* The `HeadCrownGreed` entity: `{ unlessGiven = true }`
* The `Potion` entity: `{ unlessGiven = true }`
* The `RingWonder` entity: `{ unlessGiven = true }`
* The `ShovelCrystal` entity: `{ unlessGiven = true }`



# `Switcheroo_randomizer`
This component links a player to their Switcheroo randomizer, to keep items more or less consistent between seeds and runs.

This component contains the following field:

* `entity`: entityID.

This component is hardcoded to:

* Any entity with the `controllable` component, but *not* the `Sync_possessable` component.



# `Switcheroo_soulLinkItemGen`
This component tracks item slots that are given items acros soul links, so that items are not repeatedly given.

This component contains the following field:

* `slots`: table, default `{}`. The keys of this table are slots that should be tracked and the values are [`SwEnum.SlotMark`](modules/Enum.md#SlotMark) constants representing whether items have been given in that slot.

This component is hardcoded to:

* Any entity with the `soulLinkInventory` component