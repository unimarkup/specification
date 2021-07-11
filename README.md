# Specification

This repository contains the specification of the unimarkup markup language.

The goal of unimarkup is to combine conventions of other well-known markup languages and combining them to create a markup language that can easily scale from simple README files to scientific papers or full program documentation.

The focus of unimarkup is

- Simplicity
- Consistency
- Internationalization

Unimarkup works with an implicit type system, to provide a more granular control for macros.
See [unimarkup typesystem](Unimarkup_Language_ReferenceManual.md).

For multi-language support, unimarkup sets a unique id for every block of text and stores this id with the text inside a table. Other languages are then added next to the respective entries in the table (see [internationalization and localization](###internationalization-and-localization)).

Since unimarkup is a markup language, it must be converted to other formats like pdf or html. For this, unimarkup text is first converted to a tabular representation (see [tabular representation](Unimarkup_Language_ReferenceManual.md)), and then converted to any of the supported [output formats](Unimarkup_Language_ReferenceManual.md).

Besides the language specification, there is also a specification for programs and libraries that convert unimarkup to get consistency across programing languages, operating systems and editors.

# Credit

This language was heavily influenced by the Pandoc-Flavor of Markdown, reStructuredText and Latex.

# Language Overview

Below is only a short overview of the unimarkup language, the full reference manual can be found [here](Unimarkup_Language_ReferenceManual.md).

## Fundamentals
### Headers

Headers are in atx-style only with support for 6 heading-levels. For more details, see [LRM-Headers](Unimarkup_Language_ReferenceManual.md##Headers). A header must have an emtpy new line before and after it, or another header. Header attributes are set at the end of the header text.

**Example:**
~~~
# First Main Header

Some unimarkup text for this header...

## Nested Header

More unimarkup text for the nested header...

# Second Main Header
## Other Nested Header

Even more unimarkup text...

# Header with attributes {header attributes}

# Multiline
header is also possible

The first paragraph of this header level starts here.

# Multiline
header with
additional attributes {header attributes}

# Header with explicit identifier {#explicit-header-id}

~~~

### Inline formatting

Inline formatting is applied to a paragraph. For multi-paragraph formatting see [here](###attribute-blocks).

- Bold

  A text is bold by surrounding it with `**`.
  ~~~
  **bold text**
  ~~~

- Italic

  A text is italic by surrounding it with `*`.
  ~~~
  *italic text*
  ~~~

- Underlined

  A text is underlined by surrounding it with `__`.
  ~~~
  __underlined text__
  ~~~

- Strikethrough

  A text is strikethrough by surrounding it with `~~`.
  ~~~
  ~~strikethrough text~~
  ~~~

- Verbatim

  A text can be defined verbatim by surrounding it with `.
  ~~~
  `verbatim text`
  ~~~

- Math

  Inline math mode can be used by surrounding formulas with `$`.
  ~~~
  $\frac{1}{n}$
  ~~~

### Bullet lists

Any of the characters `-+*` at start of a line followed by a space or attribute block is treated as bullet list.

Text that is indented by 2*list-depth spaces, is part of the list content of this depth.

A single backslash at start of a line between two lists separates those two lists at the highest depth.

~~~~
- Bullet list
  - Sub bullet list

- Other bullet list

  Paragraph for this bullet list

  Other paragraph for this bullet list

  ~~~
  Verbatim block for this bullet list
  ~~~

  - Sub bullet list {bullet list attributes}

    Paragraph for this sub bullet list

+ Bullet list with different symbol
  * Sub bullet list with different symbol

* Bullet list with id {#bullet-list-id}
  - Sub bullet list indented 2 spaces 

Paragraph not for a bullet list

- Bullet list with text
  that spans multiple lines
  but new lines are treated as spaces

\

- Backslash above defines this as new bullet list
~~~~

### Numbered lists

Same as bullet lists, except that enumeration items are used. Numbered lists also get automatically incremented per new item in the list and allowing to have the parent number prefixed to the sub list.

The following enumerations are allowed:

- `1.` : Numbered integer list that gets incremented by 1 per new item
- `i.` : Roman character list
- `a.` : Latin character list. After `z`, it goes to `aa`.

Besides a `.`, it is also possible to use `)`, or surround it like `(1)`, but it must be consistent inside a list.

It is also possible to start at a specific number, but this must be used for new items. Otherwise a new list is started.

~~~~
1. Start of numbered list
  1. Sub numbered list

1. Second entry in numbered list

  Paragraph for this numbered list

  Other paragraph for this numbered list

  ~~~
  Verbatim block for this numbered list
  ~~~

  1. Sub numbered list

    Paragraph for this sub numbered list

i. Numbered list with roman symbols
  i. Sub numbered list with roman symbols

a. Numbered list with latin symbols
  a. Sub numbered list with latin symbols

a. Numbered list with latin symbols
  a. Sub numbered list with latin symbols {numbered list attributes}

1. Numbered list with id {#numbered-list-id}
  1. Sub numbered list indented 2 spaces

Paragraph not for a numbered list

1. Numbered list with text
  that spans multiple lines
  but new lines are treated as spaces

\

1. Backslash above defines this as new numbered list

1. Numbered list
  1.1. Sub numbered list where the first number is for the parent numbered list
    1.1.1. Sub-sub numbered list
    
      Paragraph for the sub-sub numbered list


1) Numbered list with different style
  1)1) Sub list with parent number
1) Second item of this list
1. doesn't create a new list, but treats it as the item paragraph of the item above

(a) Numberbered list
  (a)(a) Sub numbered list with parent number

3. Numbered list starting at specific number
3. Numbered list item that gets incremented automatically
~~~~

### Combine bullet and numbered lists

Bullet and numbered lists can be changed at any depth. If the list type changes at the same depth, it is treated as a new list.

~~~
- Bullet list
  1. Sub numbered list

1. New numbered list
  - Sub bullet list
~~~

### Task lists

~~~
-[ ] Open task
-[x] Completed task (small `x`)
-[o] Active task that is worked on (small `o`)   
-[/] Failed task
~~~

### Tables

Unimarkup uses grid tables with extended flexibility.

Most notably, columns don't need to align. This helps for easier styling, since some characters are used as keywords, so the table might have more text in Unimarkup, than what is displayed after rendering. A sideeffect of this is, that `|` must be escaped when used inside a table, even in verbatim and math blocks to get the possibility of multi line rows.

The table width adapts itself by taking the rendered width of the first column and scaling the other columns according to the first line ratio of the table columns.

`+___+` marks that no line will be created between two rows, creating a multi-row.

~~~

+--+-+--+
| First column of table | 1/2 length | same length as first |
+-------+

+-+-+
| Multi row | row 1 |
+_+-+
| paragraph | row 2 |
+---+

+:-+:-:+-:+
| left alignment with `+:---+` | center alignment with `+:--:+` | right alignment with `+--:+` | 
+---------+

+-+-+-+
| number of | must match | to create |
+---+-+
| multi column | that gets |
+-+---+
| the combined | columns from the line above |
+-----+

+-{column1 attributes}+-{column2 attributes}+{row1 attributes}
| column1 row1 | column2 row1 |
+----+{table attributes}

~~~

### Verbatim blocks

3 or more `~` at start of a line mark the start and end of a verbatim block.

~~~~~
~~~~
Verbatim block, where nothing is rendered

~~~
If a verbatim block must be displayed inside a verbatim block,
the outer block must have at least one `~` more than the inner block.
~~~
~~~~

~~~{Attributes for the verbatim block}
Verbatim block with given attributes
~~~
~~~~~

### Render blocks

3 or more `'` at start of a line mark the start and end of a render block.
A render block is used to render graphics, diagramms and charts written in common graph description languages like [mermaid](https://mermaid-js.github.io/) or [opl](https://en.wikipedia.org/wiki/Object_Process_Methodology).
The language must be provided directly after the last `'` at the start of the render block.

Since OPL by default does not specify styling or referencing options, it is extended in unimarkup with the following additions:

- `is object` to define that the given name is an object
- `is process` to define that the given name is a process
- Attribute block at line end

  This is useful to link an object or process to another graph where it is described in more detail for example. Or to provide additional styling information to color an object or process to show test coverage for example.

~~~
'''mermaid
graph TB
    A & B--> C & D
'''

'''opl{<render block attributes>}
Unimarkup is object, informatical and systemic.
Pdf is object, informatical and systemic.
Html is object, informatical and systemic.
Converting is process, informatical and systemic.{#main-converting-process}
Converting consumes Unimarkup.
Converting yields Html and Pdf.
'''
~~~

### Math blocks

~~~
Blocked math mode
$$x = \frac{3}{4}$$
~~~

Math block mode inside a paragraph:
~~~
Blocked math mode $$x = \frac{3}{4}$$ can be inside a paragraph, but it will be rendered as a new line.
~~~

So the above is equivalent to:
~~~
Blocked math mode

$$x = \frac{3}{4}$$

can be inside a paragraph, but it will be rendered as a new line.
~~~

### Horizontal line

Set `-` 3 or more times on a line that is surrounded by blank lines.

~~~

---

~~~

### Hyperlinks

~~~
[Text represented as hyperlink](url){<optional hyperlink attributes>}
~~~

### File insert

~~~
![Alternative Text for this file](filepath){<optional insert attributes>}
~~~

### Comments

Unimarkup provides line comments using `****`.

**Note:** It is not possible to have a backslash at the end of a line to get a explicit new line, when a comment is used.

~~~
**** comment to end of line

A comment can be **** end of line comment
at the end of a line
~~~

### New page

At least 4 `:` at start of a line surrounded by blank lines

~~~

::::

::::{new page with attributes}

~~~

## Advanced
### Text blocks

~~~
[
  Everything inside is treated as unimarkup text.
  Provided attributes apply to all text inside this block
]{Attributes for the text block}
~~~

### Referencing

~~~
It is possible to cite using [&someRef]_.
Specify them directly, or from a bibtex file [&bibtexref]_

_[&someRef] Citation text 
~~~

### Footnotes

Footnote content will be rendered at the end of the page before the footer content where the content of a footnote is defined. If there is no new page specified, footnotes are printed at the end of the document.

**Note:** Footnotes are lost after the footnote content is rendered, so the footnote-id can be reused per page for example.

~~~
Referencing a footnote [^1]_ [^note]_.

_[^1] Here is the content of the footnote
_[^note] A note
_ can span several
_ lines
~~~

### Endnotes

Endnotes content will be rendered at the end of a header level at which the endnote content is defined.

~~~
# Header 1

Referencing an endnote [1^]_.

## Sub Header 1

Referencing an endnote in a sub header [note^]_.

## Sub Header 2

Some more text.

_[1^] Here is the content of the endnote
_
_ It is rendered before Header 2

_[note^] Here is the content of the endnote
_
_ It is also rendered before Header 2

# Header 2

Some other text
~~~

### Abbreviations

~~~
Some text with an [:abbr:]. Abbreviations must be defined surrounded by blank lines, or by other abbreviation definitions.
It is possible to render a list of all abbreviations used inside a document using the macro {@abbr}.

[:abbr:](Abbreviation)

[:xml:](Extensible Markup Language)
[:html:](Hypertext Markup Language)

~~~

### Attribute blocks

~~~
{Attribute options}
~~~

### Quotation blocks

~~~
> Block quote
> with new lines
> treates as spaces
> as with normal paragraphs
>
> > Nested block quote
~~~

### Line blocks

~~~
| Text where spaces are preserved as is.
|    All other markup however, is considered as unimarkup text.
~~~

**Note:** There is no nesting for line blocks.

### Definition blocks

~~~
: Definition term :
:
: Definition of this term
: can span multple lines

: New definition :
:
: Paragraph 1
:
: Paragraph 2

: New definition
: spanning several lines :
:
: Paragraph for this definition

: Main definition :
:
: Paragraph for the main definition.
:
: : Sub definition :
: :
: : Paragraph for the sub definition
:
: Other paragraph for the main definition
~~~


### Preamble

It is possible to define a preamble at the start of a file.

~~~
***
file preamble
***

~~~

### Direct unicode

~~~
<U+1F642>
~~~

## Dynamics
### Flags

~~~
[§flag1§ Text that gets rendered, if flag1 is set]
{§flag1§ Attributes that are applied, if flag1 is set}
~~~

### Macros

A macroname can not start with `__`, since it is reserved for internal macros.

~~~
A text that uses {@myMacro}.

This text{@sup{Is superscripted}}
~~~

### Internationalization and localization

Using the attribute block, it is possible to specify identifiers to blocks of text explicitly. Otherwise identifiers are added implicitly by unimarkup. Every text is then stored in a table with its identifier. New languages can be added, by adding the translated texts into a new column.

