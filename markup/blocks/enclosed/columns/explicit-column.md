# Explicit column block

**WIP**

Explicit column blocks have `|` as keyword.
Inside an explicit column block, a new column is started after a [line break](/markup/blocks/separators/line-break.md).

To nest explicit column blocks, the inner block must have at least one more `|` than the outer one.

**Usage:**

```
|||
This content is part of the **first** column.

:::

This content is part of the **second** column

:::

This content is part of the **third** column
|||

|||
First column is on the most right.

:::

This column is to the left side of the first column

|||{ direction : rtl }

|||
Column 1 content

:::

Column 2 content
|||{<attributes for the explicit column block>}

|||
Some content.

:::

||||
Nested column block

:::

Second column of the nested column block
||||
|||
```

**Type:** `explicit-column-block`
