# Quotation block

Quotation blocks use `>` as keyword, and may be used to quote longer text sections.
Consecutive lines may start with `>` at the same initial indentation level, but must not create a new quotation block.

**Note:** For better readability, consecutive lines should not start with `>`. 

**Note:** Attributes may be set to quotation block content, but those attributes only apply to the block content they are set to. There is no overall attribute block position for quotation blocks.

**Usage:**

```
> Block quote
  with new lines
  *treated* as spaces
  as with normal paragraphs
  and other **inline formatting** syntax is also possible.

  > Nested block quote\
    A backslash at the end of a line creates a new line.

> Some quoted text
```

**Type:** `quotation-block`
