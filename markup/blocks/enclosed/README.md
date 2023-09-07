# Enclosed blocks

**WIP**

This section contains enclosed block elements.
Enclosed blocks have start and end keywords that must start at a new line.
Both start and end keywords must have the same length, with a minimum keyword length of three. 
The block content may then start at the beginning of the line after the start keyword.
The start and end keyword lines count as blank lines for inner block elements.

To nest enclosed blocks that allow nesting, the inner keywords must be at least one grapheme longer than the outer ones for blocks having the same keyword for start and end.
Blocks with different keywords for start and end may be nested with the same keyword length for outer and inner blocks.
Increasing the inner length makes it easier to add nested blocks, because the outer keywords must not be changed.

Attributes may be set directly after the end keyword without any whitespace between.

An enclosed block must be taken as plain text paragraph, if the end keyword is not found at the end of input, or if the outer block in a nested or indented context closes.

**Example:**

```
[[[
A paragraph that has red text color.

This paragraph also has red text color.
]]]{
    color: red;
}
```

**Type:** All enclosed block elements are subtypes of the `enclosed-block` type.
