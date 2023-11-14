# Enclosed blocks

**WIP**

This section contains enclosed block elements.
Enclosed blocks have start and end keywords that must start at a new line.
Both start and end keywords must have the same length, with a minimum keyword length of three. 
The block content may then start at the beginning of the line after the start keyword.
The start and end keyword lines count as blank lines for inner block elements.

To nest enclosed blocks that allow nesting, the inner keyword length must differ from the outer ones by at least one grapheme for blocks having the same keyword for start and end.
Blocks with different keywords for start and end may be nested with the same keyword length for outer and inner blocks.

**Note:** Increasing the inner length makes it easier to add nested blocks, because the outer keywords must not be changed.

An enclosed block is implicitly closed if an outer block end or EOI is reached before the enclosed block reaches its end keywords.
In this case, no attributes can be set, because the end keywords are missing.
An enclosed block must be taken as plain text paragraph if it is not followed by a blank line.
Implementations may relax the requirement for blank lines after an enclosed block in case
attributes or decorators are set after the ending keywords to prevent expensive rollback during parsing. 

Attributes or block decoration may be set directly after the end keyword without any whitespace between.
Those decorators may again be implicitly closed if an outer block end or EOI is reached before the decorators reach their end keywords.

**Example:**

````
[[[
A paragraph that has red text color.

This paragraph also has red text color.
]]]{
    color: red;
}

- list entry

    ```
    implicitly closed verbatim block
````

**Type:** All enclosed block elements are subtypes of the `enclosed-block` type.
