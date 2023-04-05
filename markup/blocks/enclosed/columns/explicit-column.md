# Explicit column block

**WIP**

Explicit column blocks have `|` as keyword.
Inside an explicit column block, a new column is started after a [section break](/markup/blocks/separators/section-break).

To nest explicit column blocks, the outer block must have at least one more `|` than the inner one.

**Usage:**

```
|||
This content is part of the **first** column.

:::

This content is part of the **second** column

:::

This content is part of the **third** column
|||

|||{ direction : rtl }
First column is on the most right.

:::

This column is to the left side of the first column

|||

|||{<attributes for the explicit column block>}
Column 1 content

:::

Column 2 content
|||

||||
Some content.

:::

|||
Nested column block

:::

Second column of the nested column block
|||
||||
```

**Type:** `explicit-column-block`
