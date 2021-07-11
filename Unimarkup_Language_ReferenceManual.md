
# File structure
## Preamble

`.unimarkup` to provide preamble implicitly.

### Preamble sections

# Fundamentals
## Paragraph

A text with at least one character followed by one or more blank lines, or file end. 
A backslash `\` at the end of a line, creates a new line explicitly inside one paragraph.

**Examples:**

- Normal Paragraph

  ~~~
  This is a normal paragraph.
  New lines are treated as spaces,
  so this paragraph might be rendered on one line.
  ~~~

- Paragraph with explicit new line

  ~~~
  This is a normal paragraph\
  with explicit multiple line
  an a normal new line that gets treated as a space.
  ~~~

## Headers

Headers are in atx-style only with support for 6 heading-levels.
A `#` at start of a line followed by a space and one or more characters marks a header. Adding `#` before the space increases the header-level.

At least one space must be between `#` and the header and a blank line must come before and after the header, if the previous or next line is not a header. Text after a header without a blank new line is treated as header text, allowing multiline header text.

To easily link to headers, references are created implicitly, where spaces between characters get replaced by `-` and other special keywords or blocks are removed.

**Example:**

- Valid Header

  ~~~
  # First Main Header

  Some text...
  
  ## Nested Header

  More text...
  
  # Second Main Header
  ## Other Nested Header

  Even more text...
  ~~~

- Invalid Header

  ~~~
  # First Main Header
  Text still treated as header text!

  Some text...
  ## No blank line before header
  More text...
  
  #No space between # and character
  ## Other Nested Header
  Even more text...
  ~~~

## Emojis

Some special character sequences are reserved for direct emoji conversion. Those sequences must be surrounded by whitespaces.

**Full list of available emojis:**

- `:)` ... 🙂 (U+1F642)
- `;)` ... 😉 (U+1F609)
- `:D` ... 😃 (U+1F603)
- `^^` ... 😄 (U+1F604)
- `=)` ... 😊 (U+1F60A)
- `:(` ... 🙁 (U+1F641)
- `;(` ... 😢 (U+1F622)
- `:P` ... 😛 (U+1F61B)
- `;P` ... 😜 (U+1F61C)
- `O:)` ... 😇 (U+1F607)
- `:O` ... 😨 (U+1F628)
- `>:(` ... 🤬 (U+1F92C)
- `:/` ... 😕 (U+1F615)
- `3:)` ... 😈 (U+1F608)
- `-_-` ... 😑 (U+1F611)
- `<3` ... ❤ (U+2764)
- `(Y)` ... 👍 (U+1F44D)
- `(N)` ... 👎 (U+1F44E)

~~~
A text with an emoji :D in it!
~~~

Rendered to:
~~~
A text with an emoji 😃 in it!
~~~

# Special characters
## Special characters in every context

The following characters must always be escaped using a backslash if one wants to use them as plain text, except in verbatim or math mode:

- `[{}]\*`

## Special characters in a specific context

The following characters must only be escaped by a backslash in the given context:

- `()`: At block end for a possible link
- `§` : At block start until end of flagname
- `_` : When used twice to mark start or end of a underlined paragraph
- `!` : Between `[` and `§` as flag negation
- `@` : At block start for macros
- `#` : At start of a header
- `$` : When directly followed by a valid latex math symbol or another `$` and inside math mode
- `|` : Inside a table (even inside verbatim or math blocks), or at start of a new line
- `-` : At start of a new line marking a bullet list
- `~` : When used twice to mark start or end of a strikethrough paragraph, or three times or more to mark a verbatim block
- `+` : At start of a new line marking a bullet list
- `:` : After a `{` inside a macro definition and before a `}`, used to specify parameters
- `>` : At start of a new line

## Escaping special characters

All characters except spaces can be escaped using a backslash before them. Escaping characters always means that the escaped character is taken literally. There is no special meaning for `\n` or `\t` for example.

**Examples:**
~~~
\\ gets rendered to \
\$ gets rendered to $
\n gets rendered to n
~~~

# Text Block Mode

~~~
[<Unimarkup text>]
[<Unimarkup text>]{<general options>}
~~~

# File Insert

Supported types

- Images
- Videos
- Unimarkup
- Programing languages
  - Ada
  - Python
  - C#
  - C/C++
  - Java
  - Javascript
  - Rust

~~~
![<alternative text>](<filepath>){<file options><general options>}
~~~

## File options

- `parse=<parse options>`
  
  Parse options depend on file type:

  - `verbatim`
  - `embed` : svg embedding, or javascript in script-tags in HTML
  - `unimarkup`
  - `javaDoc`: Uses the JavaDoc syntax
  - `adaDoc`
  - `python`

- `highlight=(true | false)`


# Flags

Flags can contain any character except `§\` and spaces.
Flags are given either in the preamble, or as arguments for conversion programs.

~~~
[§flag§ <unimarkup text>]
{§flag§ <unimarkup attributes>}
~~~

**Flag-Negation:**
~~~
[!§flag§ <unimarkup text>]
{!§flag§ <unimarkup attributes>}
~~~


# Macros

Macroname can have any character except `{}@` and spaces and must not start with `__`.

Macros are either defined in a separate file, or inside the macro section of the [preamble](##preamble-sections).

## Usage

Defining macros:
~~~
all@macroname[]

paragraph@macroname{<type> parmetername1}{<type> parametername2}[
This is a paragraph {:parametername1:} 
]
~~~

Using macros:
~~~
{@macroname}
{@macroname{<type parmetername1>}{<type parametername2>}}
~~~

`type` defines what kind of text is allowed to be passed to the macro, and what type the macro returns.


## Predefined macros

- `{@sub{paragraph p}}`: This macro applies a subscript around the given paragraph
- `{@sup{paragraph p}}`: This macro applies a superscript around the given paragraph
- `{@mark{paragraph p}}`: This macro highlights the given paragraph
- `{@space}`: This macro adds one non-breaking space
- `{@repeat{all text, integer count}}`: This macro repeats a given text for `count`times
- `{@tab}`: This macro adds two non-breaking spaces
- `{@header{all text}}`: This macro defines a header that is applied to a page. It can be overwritten at any point, only the last macro call is taken for the header
- `{@footer{all text}}`: This macro defines a footer that is applied to a page. It can be overwritten at any point, only the last macro call is taken for the footer
- `{@toc}`: This macro inserts the table of contents at this position
- `{@refs}`: This macro inserts references used in the document at this position
- `{@abbr}`: This macro inserts abbreviations used in the document at this position

# Types

Unimarkup uses types for a more precise usage of macros.

- all
- paragraph
- inline
  - inline_bold
  - inline_italic
  - inline_underlined
  - inline_math
  - inline_strikethrough
  - inline_verbatim
- header
- table
  - table_row
  - table_entry
- list
  - list_bullet
  - list_numbered
  - list_task
- fileinsert
- hyperlink
- comment
- new_page
- block
  - block_text
  - block_math
  - block_verbatim
  - block_render
  - block_attribute
  - block_flag
  - block_quotation
  - block_line
  - block_definition
- reference
  - reference_definition
  - reference_use
- footnote
  - footnote_definition
  - footnote_use
- endnote
  - endnote_definition
  - endnote_use
- abbreviation
  - abbreviation_definition
  - abbreviation_use
- preamble
- unicode
- number
  - integer
    - natural ... 0 included
    - positive ... 0 not included
    - negative
  - decimal

To combine multiple types except *all*, types can be enclosed in braces and separated by a vertical bar.

~~~
(paragraph|table|block_math)
~~~


