
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

To easily link to headers, references are created implicitly, where Latin characters are set to lower case, spaces between characters get replaced by `-` and other characters are removed. If the resulting ID is already present, it must be set explicitly.

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
  Reference to the first header [##first-main-header]
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
- `§` : At block start until end of flag name
- `_` : When used twice to mark start or end of an underlined paragraph
- `!` : Between `[` and `§` as flag negation
- `@` : At block start for macros
- `#` : At start of a header
- `$` : When directly followed by a valid latex math symbol or another `$` and inside math mode
- `|` : Inside a table (even inside verbatim or math blocks), or at start of a new line
- `-` : At start of a new line marking a bullet list
- `~` : When used twice to mark start or end of a strike through paragraph, or three times or more to mark a verbatim block
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
[<Unimarkup text>]{<text block attributes>}
~~~

# File Insert

Supported types

- Images
- Videos
- Unimarkup
- Programming languages
  - Ada
  - Python
  - C#
  - C/C++
  - Java
  - JavaScript
  - Rust

~~~
![<alternative text>](<image url>){<image insert attributes>}
~~~

## File options

- `parse=<parse options>`
  
  Parse options depend on file type:

  - `verbatim`
  - `embed` : SVG embedding, or JavaScript in script-tags in HTML
  - `unimarkup`
  - `javaDoc`: Uses the Javadoc syntax
  - `adaDoc`
  - `python`

- `highlight=(true | false)`


# Flags

Flags are given either in the preamble, or as arguments for conversion programs.

Flags provide the possibility to control the rendered output. They are set in the preamble and can be used on text or attribute blocks.

Flags can contain any character except `?\` and spaces.

Since flags represent a boolean condition, it is possible to combine several flags using boolean logic.

**Logical operations with flags:**

- **OR** ... `?flag1? | ?flag2?` means (flag1 OR flag2)
- **AND** ... `?flag1? & ?flag2?` means (flag1 AND flag2) 
- **NOT** ... `!?flag1?` means (NOT flag1)
- **Precedence** ... `(?flag1? & ?flag2?) | ?flag3?` means (Either flag1 AND flag2, OR flag3)

~~~
[?flag1? Text that gets rendered, if flag1 is set]
{?flag1? Attributes that are applied, if flag1 is set}
~~~

# Attributes

Attributes are given in [JSON-Format](https://www.json.org/json-en.html). There are default attributes that are valid for all unimarkup elements and some specific ones for certain elements.

~~~
{<Attributes>}
~~~

Default values for all attributes can be set in the file [preamble](##preamble) or in an external file, linked in the [preamble](##preamble).

To reset attributes to their default values, write `""` for single value elements, `[]` for arrays and `{}` for objects. If attributes are not set, default values are used, but resetting can be useful, if some parent changed attribute values that can be inherited.

## General attribute units

Since attributes are defined in JSON-format, there are objects with elements that can have the same attribute units.

**List of general attribute units:**

- `"<color unit>"`

  It is possible to set colors using

  - `rgba(<0-255>,<0-255>,<0-255>,<0.0-1.0>)` in the form `red, green, blue, alpha`
  
  - `rgb(<0-255>,<0-255>,<0-255>)` where alpha is set to `1.0`

  - `#RRGGBBAA` in hexadecimal values from `00` to `FF` for `RR` red, `GG` green, `BB` blue and `AA` alpha
  
  - `#RRGGBB` in hexadecimal values where alpha is set to `FF`

  - `hsla(<0-360>,<0-100%>,<0-100%>, <0.0-1.0>)` in the form `hue, saturation, lightness, alpha`

  - `hsl(<0-360>,<0-100%>,<0-100%>)` where alpha is set to `1.0`

  Alpha refers to the transparency value with `1.0` and `FF` having no transparency.

- `"<size unit>"`

  Size units are used to define the height or width of an item. A size is given as a decimal value followed by a unit abbreviation (e.g. `16pt`, `1.5em`, `10mm`).
  
  There are two main categories of size units:

  - Absolute units

    - `cm` ... Centimeter
    - `mm` ... Millimeter
    - `in` ... Inch (2.54 cm)
    - `pt` ... Point (1/72 inch)

  - Relative units

    - `em` ... Relative to the font-size of the item (2em = 2 times the size of the current font)
    - `rem` ... Relative to the base font-size of the document
    - `%` ... Relative to the size of the parent item
    
## Default attributes

- `"id" : "<identifier name>"`
  
  The identifier name must contain at least one character, cannot start with a number, and must not contain whitespaces. The name is case-sensitive and must be unique in the generated document.
  (The same constraints as with the [HTML ID attribute](https://www.w3schools.com/html/html_id.asp))

  Additionally, the identifier name must be unique for all items inside one generated document. If several unimarkup files are combined, the identifier name must be unique across all.

- `"class" : [ "class-name-1", "class-name-2", ... ]`

  Classes that can be used to provide attributes for different items.

- `"ref" : { }`
  
  - `"label" : "<paragraph>"`

    The given paragraph can be used when referencing this item.

  - `"prefix" : "<paragraph>"`

    It is possible to set or remove a paragraph for items, which would be prefixed when referenced.

- `"padding" : { }`

  Define the space being added between the content and border of an item using padding.

  - `"all" : "<size unit>"`

    Applies the same padding to all four sides.

  - `"top" : "<size unit>"`

    Applies the padding to the top side overwriting `all`.

  - `"bottom" : "<size unit>"`

    Applies the padding to the bottom side overwriting `all`.

  - `"left" : "<size unit>"`

    Applies the padding to the left side overwriting `all`.

  - `"right" : "<size unit>"`

    Applies the padding to the right side overwriting `all`.

- `"margin" : { }`

  Define the space being added between the border of an item and the outer frame where other item frames start using margin.

  - `"all" : "<size unit>"`

    Applies the same margin to all four sides.

  - `"top" : "<size unit>"`

    Applies the margin to the top side overwriting `all`.

  - `"bottom" : "<size unit>"`

    Applies the margin to the bottom side overwriting `all`.

  - `"left" : "<size unit>"`

    Applies the margin to the left side overwriting `all`.

  - `"right" : "<size unit>"`

    Applies the margin to the right side overwriting `all`.
  
- `"border" : { }`

  Set a border for an item. 

  - `"radius" : { }`
 
    Border-radius of an item.

    - `"all" : "<size unit>"`

      Applies a radius to all four corners.

    - `"top-left" : "<size unit>"`

      Applies a radius to the top left corner overwriting `all`.

    - `"top-right" : "<size unit>"`

      Applies a radius to the top right corner overwriting `all`.

    - `"bottom-left" : "<size unit>"`

      Applies a radius to the bottom left corner overwriting `all`.

    - `"bottom-right" : "<size unit>"`
 
      Applies a radius to the bottom right corner overwriting `all`.

  - `"all" : { }`

    Border attributes that apply to all four sides.

    - `"color" : "<color unit>"`

      Border-color of an item.

    - `"style" : "<border style option>"`

      Border-style with the following options:

      - `none` ... no border
      - `dotted` ... dotted border `......`
      - `dashed` ... dashed border `------`
      - `solid` ... solid border `______`
      - `double` ... double border `======`

    - `"width" : "<size unit>"`

      Border-width of an item.

  - `"top" : { }`

    Attributes for the top border. Overwrites the values of `all`.
    Same attributes of `all` are available.

  - `"bottom" : { }`

    Attributes for the bottom border. Overwrites the values of `all`.
    Same attributes of `all` are available.

  - `"left" : { }`

    Attributes for the left border. Overwrites the values of `all`.
    Same attributes of `all` are available.

  - `"right" : { }`
 
    Attributes for the right border. Overwrites the values of `all`.
    Same attributes of `all` are available.

  - `"image" : { }`

    An image can be set as border.

    - `"source" : "<url to border-image>"`

      URL where to find the border-image.

    - `"width" : "<size unit>"`

      Width of the border-image.

    - `"scale" : "<border scale option>"`

      Define how an image is scaled, if it does not fill the complete border.

      - `"stretch"` ... The image is stretched to fill the border
      - `"repeat"` ... The image is repeated to fill the border

- `"background" : { }`

  The background object has several values. If a value is not set, the parent value is taken (At document level, the parent value is the default value).

  - `"color" : "<color unit>"`

    The background-color of an item.

  - `"image" : [ "<url to image1>", "<url to image2>", ... ]`

    One or more images that are used as backgrounds. Replaces the background-color.

## Text attributes

Text attributes are available for all text type items.

- `"text" : { }`

  - `"font" : ["<font family1>", "<font family2>", ...]`

    Several font families can be set. The first font that is available starting from left is taken. It is also possible to provide generic font family names and a matching available font is then used.

  - `"size" : "<size unit>"`

    The text-size.

  - `"weight" : "(100|200|300|400|500|600|700|800|900)"`

    Adds a weight to the text overwriting inline formatted **bold**.

    The value `100` means very light characters and `900` very bold.
    `400` is for normal characters and `700` is the default for **bold**.  

  - `"italic" : "(true|false)"`

    Sets the text as italic when `true` is set.

  - `"color" : "<color unit>"`

    The text-color.
  
  - `"spacing" : { }`

    - `"character" : "(<size unit>|kerning)"`
    
      Define the spacing between characters. `kerning` uses character spacing information from fonts that provide it.

    - `"word" : "<size unit>"`

      Define the spacing between words.

  - `"line-height" : "<size unit>"`

    The vertical line height where the text is centered in the middle.

  - `"alignment" : "<alignment option>"`

    The alignment of a text can have the following values:

    - `left` ... text is aligned to the left
    - `right` ... text is aligned to the right
    - `center` ... text is centered
    - `justify` ... every line has the same width

  - `"align-last" : "<alignment option of last line>"`

    Define how the last line is aligned, if the text alignment is set to `justify`.
    Otherwise, `align-last` has the same option as `alignment`. 

    Possible options are:

    - `left` ... last line is aligned to the left
    - `right` ... last line is aligned to the right
    - `center` ... last line is centered
    - `justify` ... last line has the same width as previous text lines

  - `"line-decoration" : { }`

    This attribute defines the line appearance that can be set for a text like underline, overline and strike through.

    - `"color" : "<color unit>"`

      Sets the line-color. If not set explicitly, the text-color is used.

    - `"style" : "<line styling option>"`

      Possible line styles are:

      - `solid`
      - `double`
      - `dotted`
      - `dashed`
      - `wavy`
      
  - `"first-indent" : "<size unit>"`

    Size of the indentation of the first line of a text.

  - `"justify-method" : "<justify method option>"`

    Defines the justification method used for `justify` alignment.

    Possible options are:

    - `auto` ... The best method is automatically determined
    - `inter-word` ... Increases/Decreases spacing between words

      **Note:** This overwrites the `word` attribute in the `spacing` object.

    - `inter-character` ... Increases/Decreases spacing between characters

      **Note:** This overwrites the `character` attribute in the `spacing` object. 

  - `"word-break" : "<(true|false)>"`

    `word-break` defines, if a word can be broken at any character at the end of a line (`true`) to prevent an overflow, or if words can't be broken up (`false`).

## Block attributes



## Attribute hierarchy

Different attributes can be applied at every level. If there are overlapping attribute values, the most local one is taken.

# Macros

Macro name can have any character except `{}@` and spaces and must not start with `__`.

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

- `{@space}`: This macro adds one non-breaking space
- `{@repeat{positive count, all text}}`: This macro repeats a given text for `count`times
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


