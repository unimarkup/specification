# Implicit column block

Implicit column blocks, like [explicit column blocks](/markup/blocks/enclosed/columns/explicit-column.md), have `|` as keyword, but allow to set a fix number of columns.
For this, the sequence `<number of columns>|` must be set directly after the start sequence of the column block, and `#|` must be set directly after the closing sequence.

To nest implicit column blocks, the inner block must have at least one more leading `|` than the outer one.

**Note:** [line breaks](/markup/blocks/separators/line-break.md) inside implicit column blocks must be treated as regular page breaks.

**Usage:**

```
|||<number of columns>|
content that is distributed over the set number of columns
|||#|{<implicit column block attributes>}

|||2| 
This content may have any form of unimarkup content. It is automatically distributed over two columns.

# Header

- Bullet list
- Inside a column block

# Header2

Some *more* text.
|||#|

|||2|
It is possible to add nested columns

||||3|
This content is inside a nested column block.
||||#|
|||#|
```

**Type:** `implicit-column-block`
