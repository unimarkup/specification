# Text block

Text blocks use `[` as opening keyword, and `]` as closing keyword.
The number of `[` and `]` must match per block.

When nesting text blocks, the inner block may have the same keyword length as the outer one.
It is just important that start and end keyword length match per block.

Attributes may be set directly after the last closing `]`.

**Note:** If no attributes are set, content inside the text block is taken as plain text.
In contrast to [verbatim blocks](/markup/blocks/enclosed/verbatim-block.md), whitespace is converted as in [paragraph blocks](/markup/blocks/paragraph.md).

Attributes for Unimarkup elements may be set as attributes of the text block,
by nesting these element attributes using the element type as identifier.
These attributes are then only applied inside the text block.

**Note:** Attribute nesting allows setting attributes for line blocks and lists, because it is not possible to set attributes for them directly.

**Note** Attribute nesting is defined in the [attributes](/markup/decorators/attributes.md) section.

**Usage:**

````
[[[
Everything inside is treated as Unimarkup content.
Provided attributes apply to all text inside this block
]]]{<Attributes for the text block>}

[[[
# Red main text block

[[[
A nested text block
]]]{ id: "main-text-block-content" }

[[[
- This bullet list has a green background

1. This numbered list has a blue background

- Again green background

This paragraph has the default background.
]]]{
     & bullet-list {
          background-color: rgb(0,255,0)
     }
     & numbered-list {
          background-color: rgb(0,0,255)
     }
}
]]]{
     & heading {
          color: rgb(255,0,0)
     }
}

[[[
Any Unimarkup text may be inside a text block

```
Verbatim block inside a text block
```
]]]{ id: "my-block" }

[[[
Text blocks without attributes.

No **formatting** is applied, since all content is taken as plain text.
]]]
````

**Type:** `text-block`
