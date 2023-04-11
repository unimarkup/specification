# Ignore file

The ignore file may contain multiple lines of element types and/or attributes
that must be ignored when rendering.

**Note:** The syntax is similar to other common ignore files like `.gitignore`.

A `!` at the start of a line marks a type or attribute to be explicitly allowed for rendering.
This is useful for hierarchical types or attributes, where the general one may be ignored,
and specific ones selectively allowed.

A `*` at any position must be treated as wildcard for *zero or more of any grapheme*.
A `?` at any position must be treated as wildcard for *exactly one grapheme*.
A `#` at the start of a line marks the line as a comment.

To provide a hierarchical structure for attributes, all attributes are preceded by `attribute/`. 
This allows to easily ignore all attributes by using `attributes/*`.

To selectively ignore element types and attributes per output format, the output format may be used as prefix, followed by `/`.

To ignore certain file formats for insertions, set the file extension after the insert-type and `/`.

**Example:**

```
# ignore all attributes for pdf output
pdf/attributes/*

# ignore media inserts for pdf output
pdf/*media*insert

# ignore all lists except bullet lists
list*
!bullet-list

# ignore JavaScript rendered insertions
*render*insert/js
```
