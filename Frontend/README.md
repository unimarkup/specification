# Introduction

This document serves as the entry point for the frontend part of the Unimarkup markup language. 
The frontend part is what the user sees when opening a Unimarkup file inside any plain text editor.

A Unimarkup frontend file has `.um` as an extension.

# Elements

Elements are the parts in Unimarkup that define character sequences to be rendered.
All elements are grouped in three main element types:

- [`inline`](Inlines.md)

  Elements that may be part of the content of other elements.
  Most common inline elements are hyperlinks, formatting and referencing.

- [`atomic-block`](AtomicBlocks.md)

  Atomic blocks are elements that may have multiple content lines, but no blank line.

- [`enclosed-block`](EnclosedBlocks.md)

  Enclosed blocks have start and end character sequences and allow blank lines as part of their content.

# Language constructs

Besides Unimarkup elements, there are also some programming language constructs available in Unimarkup.

- [Macros](Macros.md)

  Macros are similar to functions in most programming languages, and offer extended flexibility.

- [Variables](Variables.md)

  Variables may be defined either globally in a Unimarkup document, or locally inside a macro.

- [Operators](Operators.md)

  Operators are a special form of macros, offering common programming language functionalities.

# Preamble

It is possible to define a preamble block at the start of a Unimarkup file by surrounding the block with `+++`
followed by a blank line. Only one preamble is allowed per Unimarkup file and must start at the first line.

Possible options and alternative configurations are defined in the [configuration reference](../Configuration_Reference.md).

**Usage:**

```
+++
<preamble>
+++
```

**Using JSON:**

```
+++
{
    "output-file": "output.html",
    "output-formats": ["Html"],
    "html_embed_svg": true
}
+++
```

**Using YAML:**

```
+++
output-file: "output.html"
output-formats: ["Html"]
html_embed_svg: true
+++
```

# Escaping special characters

All characters may be escaped using a backslash before them.
Escaping characters always means that the escaped character is taken literally.
For example, there is no special meaning for `\n` or `\t`.

**Note:** Backslash escaping may also be used for inline verbatim to render `` ` ``.

**Note:** It is also possible to escape spaces and tabs, which are then kept as is during rendering.

**Examples:**

```
\\ gets rendered to \
\$ gets rendered to $
\n gets rendered to n

\  escapes one space

`\`` gets rendered to <verbatim start>`<verbatim end>
```

# Caption

It is possible to set a caption directly above or below an atomic or enclosed block element except headings. No blank line must be between caption and block.
A caption may only have one paragraph.
To set a caption to a block, set `+++` on a new line. To close the caption, set `+++` at a new line after the caption paragraph.
An attribute block may be set directly after the starting `+++` on the same line and may span multiple lines.
A blank line must be set before the caption, if it is set before the block, or after the caption, if it is set after the block.

**Note:** Elements with a caption must create an additional IR entry with `-caption` as postfix to the Unimarkup type of the element and content and attributes being the caption ones, but the ID is taken from the element.

**Usage:**

```
!!![figure insert](image.png)
+++{ <optional caption attributes> }
Caption of a figure
+++

===
| some table | with columns |
===
+++
Caption of a table
+++
```
