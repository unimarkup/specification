# Explicit Unicode

Any Unicode code point may be inserted in Unimarkup with `&<Unicode code point>;`. Where the *Unicode code point* is given in the form `U+<HEX value>`.

**Note:** The `U` must be interpreted case-insensitive, so `&u+<HEX value>;` must also work.

**TODO:** Link to online resource with a table of Unicode HEX values.

**Usage:**

```
&U+1F642;
```

**Type:** `explicit-unicode`
