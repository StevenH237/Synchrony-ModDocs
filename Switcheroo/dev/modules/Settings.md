`local SwSwettings = require "Switcheroo.Settings"`

*Note: This page covers the settings module for code purposes. See [Settings](../Settings.md) for the setting nodes added by the mod or [Options](../../Options.md) for an end-user settings guide.*

# `get(string): any`
* `setting`: `string` - The setting to retrieve.

Returns a setting node using PowerSettings' `get`. Automatically adds the `mod.Switcheroo.` prefix, so `SwSettings.get("allowedFloors")` is equivalent to `PowerSettings.get("mod.Switcheroo.allowedFloors")`.