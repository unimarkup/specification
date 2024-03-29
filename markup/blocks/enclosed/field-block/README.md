# Field block

This element adds a field name at the start of a [text block](/markup/blocks/enclosed/text-block.md) that is enclosed inside `<>`.
This field name may be used to provide additional built-in elements, or extend the base implementation with plugins as defined in the [plugins](/addons/plugins/README.md) section.

If a field name is not known by an implementation, the field block
must be treated as a normal [text block](/markup/blocks/enclosed/text-block.md) without the field name.

If text blocks are used inside field blocks, or field blocks allow nesting, the inner field block must have at least one more `[` than the outer one.

**Note:** Available attributes may vary between different field blocks.

**Note:** `<>` is not a placeholder in the usage examples.

**Usage:**

```
[[[<field name>
Any Unimarkup content.
]]]

[[[<someField>
Any Unimarkup content.
]]]{some attributes}
```

**Type:** All field block elements are subtypes of the `field-block` type.
