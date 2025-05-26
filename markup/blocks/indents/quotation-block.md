# Quotation block

Quotation blocks use `>` as keyword, and may be used to quote longer text sections.
Consecutive lines may start with `>` at the same initial indentation level, but must not create a new quotation block.

An author paragraph may be set at the end of a quotation block, by starting a line at the indentation level of the block content with `--` followed by at least one space.
The author paragraph must be separated by at least one blank line from the block content, and the quotation block automatically ends after the author paragraph ends.

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

    -- Author of the nested block quote

> Some quoted text
```

**Type:** `quotation-block`
