`local NixLib = require "NixLib.NixLib"`

---

# `bitSplit(value, log)`: table
* `value` (integer): The value to test
* `log` (bool): Whether or not the actual values or powers should be shown.

Splits `value` into a table of its "1" bits. For example, `bitSplit(237)` is `{128, 64, 32, 8, 4, 1}`.

If `log` is true, then all of the values in the table will be taken log base 2. For example, `bitSplit(237, true)` is `{7, 6, 5, 3, 2, 0}`.

---

# `checkFlags(value, test, all)`: bool
* `value` (integer): The value to test
* `test` (integer): The test to pass or fail
* `all` (bool): Whether all bits from `test` must be satisfied

Compares `value` and `test` as bitfields, returning `false` if `value` doesn't have any `1`s in common with `test`, and `true` otherwise.

If `all` is set, `value` must have at least all `1`s from `test` (though may have more) for a `true` result.

---

# `getComponent(name)`: table
* `name` (string): The name of the component to get

Gets a single component from the game, including its field defaults. Returns `nil` if the component doesn't exist.

---

# `getComponents()`: table

Gets the table of all components in the game, as a key-value table.

---

# `getModVersion(name)`: (nil) or (bool) or (string, bool)
* `name` (string): The name of the mod to check.

⚠️ **DEPRECATED:** I severely messed up the return values of this function; it doesn't even return its namesake. See [`isModLoaded(name)`](#ismodloadedname-bool-string-bool) for what it *should've* been; the *actual* return values are now documented below. Just to not break any mods that might already be using it, I didn't fix it yet, but this function will eventually be removed in favor of `isModLoaded`.

Return value varies based on whether or not the mod is loaded:

* `nil` if the mod list isn't loaded yet.
* `false` if the mod in question isn't loaded (but the list is).
* If the mod *is* loaded:
  * (string): The mod's name.
  * (bool): Whether or not the mod is packaged.

---

# `isModLoaded(name)`: bool, string, bool
* `name` (string): The name of the mod to check.

Returns whether or not a given mod is loaded, and if so, also the version:

* `nil` if the mod list isn't loaded yet.
* `false` if the mod in question isn't loaded (but the list is).
* `true` if the mod list and mod are both loaded. If so, has additional return values:
  * (string): The mod's version.
  * (bool): Whether or not the mod is packaged.

---

# `join(tbl, sep)`: string
* `tbl` (table): The ipairs-compatible table to join
* `sep` (string): The separator with which to join the items

Iterates over the numeric keys of the table (using `ipairs`), joining their values together with the given separator. Returns the joined string.

---

# `median(a, b, c)`: number
* `a` (number): The first number to test
* `b` (number): The second number to test
* `c` (number): The third number to test

Compares `a`, `b`, and `c`; returns the median value of the three.

---

# `sjoin(l, r, sep, force)`: string or nil
* `l` (string or nil): The item to place left of the separator
* `r` (string or nil): The item to place right of the separator
* `sep` (string): The separator to use if both `l` and `r` exist
* `force` (bool): If `true`, `sep` is *always* included. Otherwise, `sep` is only included if both `l` and `r` are non-`nil`.

Returns `l`, `sep`, and `r` as one string, if all are non-nil. Otherwise, only the non-`nil` input is included. Returns `nil` if inputs are both `nil` and `sep` is not `force`d.

---

# `sortBy(tbl, key, cmp)`: nil
* `tbl` (table): The table to sort
* `key` (function or any): The key or key-getter to sort by
* `cmp` (function?): The key comparison function

Sorts a table, in-place, by comparing a specified key in all of its objects.

If `key` is a function, it should be one that takes an object from the table as its input and produces a comparable value as its output. Otherwise, it's treated as a table index.

If `cmp` is specified, it should be a function that takes two keys and returns `true` iff the first key is less than the second. If it's not, the standard operator `<` is used instead.

This isn't a stable sort method; that is, objects considered equal may still have their relative positions changed.

---

# `sortByMany(tbl, cmp, key...)`: nil
* `tbl` (table): The table to sort
* `cmp` (function or nil): The key comparison function
* `key...` (function or any): The keys and/or key-getters to sort by

Sorts a table, in-place, by comparing specified keys in all of its objects.

If any `key` is a function, it should be one that takes an object from the table as its input and produces a comparable value as its output. Otherwise, it's treated as a table index.

If `cmp` is specified, it should be a function that takes two keys and returns either:
* `true, false` iff `a` < `b`, `false, true` iff `a` == `b`, and `false, false` iff `a` > `b`
* A number less than 0 iff `a` < `b`, 0 iff `a` == `b`, and a number greater than zero iff `a` > `b`

---

# `splitToList(str)`: table
* `str` (string): The string to split
* `sep` (string): The characters upon which to split `str`; can include pattern-escaped characters; defaults to `"%s"`.

Splits a string at its spaces (or `sep`) into a table of one-word strings. For example, `"Hello world"` becomes `{"Hello", "world"}`.

---

# `splitToSet(str)`: table
* `str` (string): The string to split
* `sep` (string): The characters upon which to split `str`; can include pattern-escaped characters; defaults to `"%s"`
* `del` (string): The string upon which to split an entry from its key; defaults to `":"`; can include pattern-escaped characters
* `def` (any): The value given to keys that do not include `del`. Defaults to `true`.

Splits a string at its spaces (or `sep`) into a table, where each word from the string is split again at a colon (or `del`) into a key/value, or treated as a key with value `true` (or `def`). For example, `"Hello:3 world"` becomes `{Hello = "3", world = true}`.

---

# `versionCompare(left, right)`: bool, bool
* `left` and `right` (string): Versions to compare.

Compares two Synchrony mod version strings. A Synchrony mod version string is any number of numeric components separated by single periods, such as `3`, `2.2.0`, or `0.0.0.0.0.1`. They compare using the following rules:

1. Identical strings are equal versions, even if they're not *valid* version strings (i.e. this rule is checked before any parsing).
2. Version string are compared by comparing all common segments from left to right numerically until a difference is found. The version string with the lower segment is the lower (earlier) version.
3. If all common segments are equal but the version strings are of uneven sizes, the string with fewer segments is the lower version.
4. If all segments are equal and the version strings are of even sizes, the version strings are equal.

Once the comparison is made, the return value is as follows:
1. (boolean): Whether or not `left` is a *lower* version string than `right`. (This allows it to be used in `table.sort`.)
2. (boolean): Whether or not the two version strings are *equal*.

Throws if the strings are not identical and either string isn't a valid version string.