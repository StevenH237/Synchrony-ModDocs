`local MenuMod = require("MenuMod.MenuMod")`

---

# `register(args)`: [nil]
Registers a submenu to be shown in MenuMod's menu container.

`args` should be a table that contains some or all of the following values:

* **`name`** (string or `func():[string]`, required): The name of the submenu as shown in MenuMod's container.
* **`menu`** (string, required): Which other menu should this option open?
* *`id`* (string, conditionally required): What should the ID be? Required iff `menu` is not a string (which may be allowable in the future).
* `subsequence` (number, optional): If one mod creates multiple submenus, this number determines their order relative to each other. 
* `visibleIf` (`func(table):[bool]`, optional): Function that determines whether or not this submenu option should be visible.
* `enabledIf` (`func(table):[bool]`, optional): Function that determines whether or not this submenu option should be enabled.
* `menuArg` (`func(table):[any]` or any, optional): What should be passed to `ev.arg` in the receiving menu event?

Some remarks:

If `name` is a function, it's evaluated every tick while ModMenu's container is open.

If `id` isn't specified, it becomes equal to `menu`.

`subsequence` only controls the order of submenus from a single mod. All submenus from one mod are grouped together, and the order of these groups is determined by MenuMod itself. Submenus without a specified `subsequence` are sorted after those *with* one specified, in order by `id`.

`visibleIf`, `enabledIf`, and `menuArg` (if it's a function) all receive a table parameter. This table contains the following. (This is also the `ev.arg` parameter for MenuMod's container):

* `source` (string): How ModMenu's container was (or is about to be) opened.

Additionally, the method used to opening ModMenu's container also determines when `visibleIf` is evaluated:

* `pause`: `visibleIf` is evaluated when the pause menu opens.
* `hotkey`: `visibleIf` is evaluated when the hotkey is pressed.

`visibleIf` is not re-evaluated when MenuMod's container is opened. Additionally, if every registered menu returns `false`, the MenuMod option will be omitted from the pause menu altogether. On the other hand, `enableIf` is evaluated when MenuMod's container is opened. If either of these arguments isn't present in the `args` table (or isn't a function), an implicit `true` is used instead.

If `menuArg` is a function, it is evaluated when the submenu is opened, and its value passed to `ev.arg` instead. (This does not happen recursively.)
