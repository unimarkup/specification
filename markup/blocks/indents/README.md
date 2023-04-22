# Indented blocks

This section contains blocks that may have indented nested content.
The indentation step for content must increase by exactly two spaces per nesting level.

This indentation creates a nesting depth that starts at `1`, and increases `+1` on every further nesting level.
The block at lower depth is referred to as `parent`.

An indented block starts with a keyword followed by one space.
The content after the space is part of the block content.

**Note:** The blank line restrictions for blocks also apply in nested content.

**Note:** An indented block ends before the first element in document flow that is not indented to the required depth.

**Type:** All indented blocks are subtypes of the `indented-block` type.

**Example:**

```
- bullet list
  1. numbered list nested in bullet list

    paragraph for the numbered list

  paragraph for the bullet list
```
