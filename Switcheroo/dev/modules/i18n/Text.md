`local SwText = require "Switcheroo.i18n.Text"`

This module contains most of the localizable strings in Switcheroo, as follows.

Prefix all translation keys with `mod.Switcheroo.text.`. I also have a repository [here](https://github.com/StevenH237/Synchrony-Translations) that contains a translation template and various languages into which the mod is translated.

# Static
These are all localizable strings themselves within the module. They contain no formatting keys.

| Module path                               | Translation key                           | English text                        |
| :---------------------------------------- | :---------------------------------------- | :---------------------------------- |
| `Bans.Giving.Allow`                       | `bans.giving.allow`                       | Allow item                          |
| `Bans.Giving.DontAllow`                   | `bans.giving.dontAllow`                   | Don't allow item                    |
| `Bans.Giving.DynamicGold`                 | `bans.giving.dynamicGold`                 | Allow while holding gold            |
| `Bans.Taking.DontTake`                    | `bans.taking.dontTake`                    | Don't take item                     |
| `Bans.Taking.Take`                        | `bans.taking.take`                        | Take item                           |
| `Bans.Taking.TakeIfGiven`                 | `bans.taking.ifGiven`                     | Take if given by mod                |
| `CharmsAlgorithms.Simple`                 | `charmsAlgorithms.simple`                 | Simple                              |
| `Floors.ExtraBossFloors`                  | `floors.extraBoss`                        | Add extra/custom boss floors        |
| `Floors.ExtraOtherFloors`                 | `floors.extraOther`                       | Add other extra floors              |
| `Floors.ExtraPostBosses`                  | `floors.extraPostBosses`                  | Add extra post-boss floors          |
| `Floors.ExtraStoryBoss`                   | `floors.extraStoryBoss`                   | Extra story boss                    |
| `Floors.Ordinal[1]`                       | `floors.ordinal.1`                        | 1st                                 |
| `Floors.Ordinal[2]`                       | `floors.ordinal.2`                        | 2nd                                 |
| `Floors.Ordinal[3]`                       | `floors.ordinal.3`                        | 3rd                                 |
| `Floors.Ordinal[4]`                       | `floors.ordinal.4`                        | 4th                                 |
| `Floors.Ordinal[5]`                       | `floors.ordinal.5`                        | 5th                                 |
| `Floors.Ordinal[6]`                       | `floors.ordinal.6`                        | 6th                                 |
| `Floors.Ordinal[7]`                       | `floors.ordinal.7`                        | 7th                                 |
| `Floors.Ordinal[8]`                       | `floors.ordinal.8`                        | 8th                                 |
| `Floors.Ordinal[9]`                       | `floors.ordinal.9`                        | 9th                                 |
| `Floors.Ordinal[10]`                      | `floors.ordinal.10`                       | 10th                                |
| `Floors.Ordinal[11]`                      | `floors.ordinal.11`                       | 11th                                |
| `Floors.Ordinal[12]`                      | `floors.ordinal.12`                       | 12th                                |
| `Floors.Ordinal[13]`                      | `floors.ordinal.13`                       | 13th                                |
| `Floors.Ordinal[14]`                      | `floors.ordinal.14`                       | 14th                                |
| `Floors.Ordinal[15]`                      | `floors.ordinal.15`                       | 15th                                |
| `Floors.Ordinal[16]`                      | `floors.ordinal.16`                       | 16th                                |
| `Floors.Ordinal[17]`                      | `floors.ordinal.17`                       | 17th                                |
| `Floors.Ordinal[18]`                      | `floors.ordinal.18`                       | 18th                                |
| `Floors.Ordinal[19]`                      | `floors.ordinal.19`                       | 19th                                |
| `Floors.Ordinal[20]`                      | `floors.ordinal.20`                       | 20th                                |
| `Floors.Ordinal[21]`                      | `floors.ordinal.21`                       | 21st                                |
| `Floors.RawFloorNumbers`                  | `floors.rawNumbers`                       | Custom dungeons use floor numbers   |
| `Floors.TrainingFloors`                   | `floors.trainingFloors`                   | Training floors                     |
| `Formats.NoLimit`                         | `formats.noLimit`                         | (No limit)                          |
| `Formats.Sell.No`                         | `formats.sell.no`                         | No                                  |
| `ItemPools.itemPoolChest`                 | `itemPools.itemPoolChest`                 | Chest                               |
| `ItemPools.itemPoolRedChest`              | `itemPools.itemPoolRedChest`              | Red boss chest                      |
| `ItemPools.itemPoolPurpleChest`           | `itemPools.itemPoolPurpleChest`           | Purple boss chest                   |
| `ItemPools.itemPoolBlackChest`            | `itemPools.itemPoolBlackChest`            | Black boss chest                    |
| `ItemPools.itemPoolLockedChest`           | `itemPools.itemPoolLockedChest`           | Locked chest                        |
| `ItemPools.itemPoolShop`                  | `itemPools.itemPoolShop`                  | Shop                                |
| `ItemPools.itemPoolLockedShop`            | `itemPools.itemPoolLockedShop`            | Locked shop                         |
| `ItemPools.itemPoolUrn`                   | `itemPools.itemPoolUrn`                   | Urn                                 |
| `ItemPools.itemPoolSecret`                | `itemPools.itemPoolSecret`                | Conjurer                            |
| `ItemPools.itemPoolFood`                  | `itemPools.itemPoolFood`                  | Food                                |
| `ItemPools.itemPoolHearts`                | `itemPools.itemPoolHearts`                | Hearts                              |
| `ItemPools.itemPoolCrate`                 | `itemPools.itemPoolCrate`                 | Crate                               |
| `ItemPools.itemPoolWar`                   | `itemPools.itemPoolWar`                   | Shrine of War                       |
| `ItemPools.itemPoolUncertainty`           | `itemPools.itemPoolUncertainty`           | Shrine of Uncertainty               |
| `ItemPools.itemPoolEnchant`               | `itemPools.itemPoolEnchant`               | Enchant weapon scroll               |
| `ItemPools.itemPoolNeed`                  | `itemPools.itemPoolNeed`                  | Need scroll                         |
| `ItemPools.Switcheroo_itemPoolSwitcheroo` | `itemPools.Switcheroo_itemPoolSwitcheroo` | Switcheroo default                  |
| `ReplaceMode.Empty`                       | `replaceMode.empty`                       | Fill empty slots                    |
| `ReplaceMode.Everything`                  | `replaceMode.everything`                  | Fill and replace                    |
| `ReplaceMode.Existing`                    | `replaceMode.existing`                    | Replace existing items              |
| `Slots.Names.Misc`                        | `slots.names.misc`                        | Charms                              |
| `Slots.Presets.AllButHolster`             | `slots.presets.allButHolster`             | All slots except holster            |
| `Slots.Presets.AllButHolsterShield`       | `slots.presets.allButHolsterShield`       | All slots except shield and holster |
| `Slots.Presets.AllButShield`              | `slots.presets.allButShield`              | All slots except shield             |
| `Slots.Presets.AllButWeapon`              | `slots.presets.allButWeapon`              | All slots except weapons            |
| `Slots.Presets.AllButWeaponShield`        | `slots.presets.allButWeaponShield`        | All slots except shield and weapons |
| `Slots.Presets.AllSlots`                  | `slots.presets.allSlots`                  | All slots                           |
| `Slots.Presets.NoSlots`                   | `slots.presets.noSlots`                   | No slots                            |

## Slot names
These will be removed from the mod iff I find a way to use existing translation keys.

| Module path           | Translation key       | English text |
| :-------------------- | :-------------------- | :----------- |
| `Slots.Names.Action`  | `slots.names.action`  | Item         |
| `Slots.Names.Body`    | `slots.names.body`    | Body         |
| `Slots.Names.Feet`    | `slots.names.feet`    | Feet         |
| `Slots.Names.Head`    | `slots.names.head`    | Head         |
| `Slots.Names.Holster` | `slots.names.holster` | Holster      |
| `Slots.Names.Ring`    | `slots.names.ring`    | Ring         |
| `Slots.Names.Shield`  | `slots.names.shield`  | Shield       |
| `Slots.Names.Shovel`  | `slots.names.shovel`  | Shovel       |
| `Slots.Names.Spell`   | `slots.names.spell`   | Spell        |
| `Slots.Names.Torch`   | `slots.names.torch`   | Torch        |
| `Slots.Names.Weapon`  | `slots.names.weapon`  | Attack       |

# Functions
These are all functions that take some number of parameters and return a localized string formatted with those parameters.

| Module path                | Translation key            | Parameters                             | English Text                  | Note                                                                                                         |
| :------------------------- | :------------------------- | :------------------------------------- | :---------------------------- | :----------------------------------------------------------------------------------------------------------- |
| `Floors.DepthLevel`        | `floors.depth`             | `%s {ord}`, `%d {depth}`, `%d {floor}` | {ord} floor ({depth}-{floor}) |                                                                                                              |
| `Formats.ItemPoolAdvanced` | `formats.itemPoolAdvanced` | `%s {poolName}`, `%s {poolID}`         | {poolName} ({poolID})         | Most languages shouldn't change this, but RTL languages may wish to make it `({poolID}) {poolName}` instead. |
| `Formats.Sell.Yes`         | `formats.sell.yes`         | `%g {percent}`                         | {percent}% of purchase price  |                                                                                                              |
| `Settings.DefaultItemDesc` | `settings.defaultItemDesc` | `%s {slot}`                            | Default item for {slot} slot  |                                                                                                              |

# Noun case function
The translation key `grammar.nounCase` has a default value of "lower". Languages like German where nouns are always capitalized should set this to "upper" instead.

The function `Func.NounCase` takes a string, then checks that translation key. If its value is "upper", the input parameter is returned unchanged (it's assumed to already be capitalized). Otherwise, the input parameter is returned all-lowercase.
