# Line block

Line blocks preserve whitespaces, but render markup as usual.
A line block is started with `|` per new line followed by one space.

**Note:** There is no nesting for line blocks.

**Note:** Since Unimarkup keywords are removed in the rendered document, the text might not align the same way in the raw and rendered form.

**Note:** Setting explicit new lines with a backslash at the end has no effect, since new lines are preserved in line blocks.

**Note:** It is not possible to set attributes for line blocks.

**Usage:**

```
| Text where *spaces* are preserved as is.
|    All other **markup** however, is considered as **Unimarkup text**.

| A verbatim block may be used inside a line block
|
| ```
| Some verbatim text
| ```
|
| Since spaces are already kept, a verbatim block inside a line block
| is only necessary to get code highlighting and prevent rendering.
```

**Type:** `line-block`
