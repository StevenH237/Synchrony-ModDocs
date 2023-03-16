# Existing code
This tutorial builds on [part 1](GettingStarted-1.md). If you want to check your code or you chose to skip part 1, you can use the following:

```lua
local Event = require "necro.event.Event"
local Settings = require "necro.config.Settings"
local Enum = require "system.utils.Enum"
local StringUtilities = require "system.utils.StringUtilities"

-- ENUMS
local cases = Enum.sequence {
  NORMAL = 0,
  UPPER = 1,
  LOWER = 2,
  TITLE = 3,
  FIRST = 4
}

-- SETTINGS
HelloEnabled = Settings.shared.bool {
  id = "helloEnabled",
  name = "Enable hello world",
  default = false,
  order = 0
}

HelloCount = Settings.shared.number {
  id = "helloCount",
  name = "Hello world count",
  minimum = 1,
  maximum = 5,
  default = 1,
  order = 1
}

HelloText = Settings.shared.string {
  id = "helloText",
  name = "Hello world text",
  default = "Hello world!",
  order = 3
}

HelloCase = Settings.shared.enum {
  id = "helloCase",
  name = "Hello world case",
  enum = cases,
  default = cases.NORMAL,
  order = 4
}

-- EVENTS
Event.levelLoad.add("settingsTest", { order = "entities" }, function(ev)
  local text = HelloText

  if HelloCase == cases.UPPER then
    text = text:upper()
  elseif HelloCase == cases.LOWER then
    text = text:lower()
  elseif HelloCase == cases.TITLE then
    text = StringUtilities.titleCase(text)
  elseif HelloCase == cases.FIRST then
    text = StringUtilities.capitalizeFirst(text)
  end

  if HelloEnabled then
    for i = 1, HelloCount do
      print(text, i)
    end
  end
end)
```

# Action settings
It's possible to make a settings menu entry that performs a function rather than changing a value. You can define the function anonymously within the setting definition, or externally earlier in the script. I'm going to go with the latter.

Add the following above the `-- SETTINGS` block:

```lua
-- ACTIONS
local function sayHello()
  local text = HelloText

  if HelloCase == cases.UPPER then
    text = text:upper()
  elseif HelloCase == cases.LOWER then
    text = text:lower()
  elseif HelloCase == cases.TITLE then
    text = StringUtilities.titleCase(text)
  elseif HelloCase == cases.FIRST then
    text = StringUtilities.capitalizeFirst(text)
  end

  if HelloEnabled then
    for i = 1, HelloCount do
      print(text, i)
    end
  end
end
```

This is indeed just the event handler at the bottom. Go ahead and remove that; we won't be using it any more.

Now, add the following to the bottom of the settings block:

```lua
SayHello = Settings.shared.action {
  id = "sayHello",
  name = "Say hello! (test)",
  action = sayHello,
  order = -1
}
```

*(Be careful that you don't write `sayHello()` here; this may seem obvious if you're already familiar with Lua, and yet that's a mistake I make all the time.)*