# Field box

This element adds a field name at the start of an inline text box that is enclosed inside `<>`.
This field name may be used for certain output formats or language extensions.
If a field name is not known by an output format, or no language extension is available to handle the field name, the inline field
is treated as a normal [inline text box](/markup/inlines/boxes/text-box) without the field name.

The [builtins](/markup/inlines/boxes/field-box/builtins) section includes field boxes that must be built-in in a Unimarkup implementation.

**Note:** `<>` is not a placeholder in the usage examples.

**Usage:**

```
[<kbd>Ctrl+C]

[<someField> Some inline content]
```

**Type:** All field box variants are part of the `field-box` type.

**Note:** Variations must have types with the form `field-box-<field name>` (`<>` are placeholders in this example).
