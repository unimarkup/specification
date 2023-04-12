# Text block

Text blocks use `[` as opening keyword, and `]` as closing keyword.
The number of `[` and `]` must match per block.
Attributes may be set directly after the last opening `[`.

To nest text blocks, the outer block must have at least one more `]` than the inner one.

Attribute values for Unimarkup elements may be set as attributes of the text block,
by nesting these element attributes using the element type as identifier.

**Note:** Attribute nesting allows setting attributes for line blocks and lists, since it is not possible to set attributes for them directly.

**Note** Attribute nesting is defined in the [attributes](/markup/decorators/attributes.md) section.

**Usage:**

````
[[[{<Attributes for the text block>}
Everything inside is treated as Unimarkup content.
Provided attributes apply to all text inside this block
]]]

[[[[{ & heading { color: rgb(255,0,0) }}
# Red main text block

[[[{ id: "main-text-block-content" }
A nested text block
]]]

[[[{ & bullet-list { background-color: rgb(0,255,0) }}
     & numbered-list { background-color: rgb(0,0,255) }}}

- This bullet list has a green background

1. This numbered list has a blue background

- Again green background

This paragraph has the default background.
]]]
]]]]

[[[
Any Unimarkup text may be inside a text block

```
Verbatim block inside a text block
```
]]]
````

**Type:** `text-block`
