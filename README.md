# Specification

This repository contains the specification of the unimarkup markup language.

The goal of unimarkup is to combine conventions of other well-known markup languages and combining them to create a markup language that can easily scale from simple README files to scientific papers or full program documentation.

The focus of unimarkup is

- Simplicity
- Consistency
- Internationalization

Unimarkup works with an implicit type system, to provide a more granular control for macros.
See [unimarkup type system](Unimarkup_Language_ReferenceManual.md).

For multi-language support, unimarkup sets a unique ID for every block of text and stores this ID with the text inside a table. Other languages are then added next to the respective entries in the table (see [internationalization and localization](###internationalization-and-localization)).

Since unimarkup is a markup language, it must be converted to other formats like PDF or HTML. For this, unimarkup text is first converted to a tabular representation (see [tabular representation](Unimarkup_Language_ReferenceManual.md)), and then converted to any of the supported [output formats](Unimarkup_Language_ReferenceManual.md).

Besides the language specification, there is also a specification for programs and libraries that convert unimarkup to get consistency across programming languages, operating systems and editors.

# Credit

This language was heavily influenced by the Pandoc-Flavor of Markdown, reStructuredText and Latex.

# Language Overview

Below is only a short overview of the unimarkup language, the full reference manual can be found [here](Unimarkup_Language_ReferenceManual.md).

## Fundamentals
### Headers

Headers are in atx-style only with support for 6 heading-levels. For more details, see [LRM-Headers](Unimarkup_Language_ReferenceManual.md##Headers). A header must have an empty new line before and after it, or another header. Header attributes are set at the end of the header text.

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

Inline formatting can also be applied inside words.

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

- Underline

  A text is underlined by surrounding it with `__`.
  ~~~
  __underlined text__
  ~~~

- Overline

  A text is overlined by surrounding it with `^_`.

  ~~~
  ^_overlined text^_
  ~~~

- Strike through

  A text is strike through by surrounding it with `~~`.
  ~~~
  ~~strike through text~~
  ~~~

- Superscript

  A text is superscripted by surrounding it with `^`.

  ~~~
  ^superscripted text^
  ~~~

- Subscript

  A text is subscripted by surrounding it with `_`.

  ~~~
  _subscripted text_
  ~~~

- Verbatim

  A text can be defined verbatim by surrounding it with `` ` ``.
  If you want to use a `` ` `` inside, you need to use ` `` ` at start and end.  
  ~~~
  `verbatim text`

  `` ` ``
  ~~~

- Math

  Inline math mode can be used by surrounding formulas with `$`.
  ~~~
  $\frac{1}{n}$
  ~~~

- Highlight

  A text can be highlighted by surrounding it with `|`.

  ~~~
  |highlighted text|
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
- `rI.` : Roman capital character list. Possible characters are `I`, `V`, `X`, `L`, `C`, `D`, `M`
- `Ri.` : Roman lower character list. Possible characters are `i`, `v`, `x`, `l`, `c`, `d`, `m`
- `a.` : Lower Latin character list. After `z`, it goes to `aa`.
- `A.` : Capital Latin character list. After `Z`, it goes to `AA`.

Besides a `.`, it is also possible to use `)`, or surround it like `(1)`, but it must be consistent inside a list.

It is also possible to start at a specific number, but this must be used for new items. Otherwise, a new list is started.

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

rI. Numbered list with capital roman symbols
  rI. Sub numbered list with capital roman symbols

Ri. Numbered list with lower roman symbols
  Ri. Sub numbered list with lower roman symbols

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

Task lists provide 4 states to represent tasks.

1. `[ ]` Open task (the space between the square brackets is important)
2. `[x]` Completed task (small `x`)
3. `[o]` Active task (small `o`)
4. `[/]` Failed task

It is possible to get nested task lists, by setting `-[] <task description>` at the higher level.
The state of the higher task depends on the states of all lower tasks.
If at least one lower task is set to fail, the higher task is set to fail. Otherwise, the higher level task is set to active, if any of the lower tasks is set to active. The higher level task is set to completed, if all lower tasks are completed. If there are no active or failed lower tasks and there is at least one open lower task, the higher task is set to open.

~~~
-[ ] Open task
-[x] Completed task
-[o] Active task that is worked on   
-[/] Failed task
-[] Nested task with status = fail
  -[x] Completed task
  -[x] Another one completed
  -[/] Failed task
  -[o] Active task
  -[ ] Open task
-[] Nested task with status = active
  -[x] Completed task
  -[o] Active task
  -[ ] Open task
-[] Nested task with status = cmpleted
  -[x] Completed task
  -[x] Completed task2
-[] Nested task with status = open
  -[x] Completed task
  -[ ] Open task
-[] Nested tasks can be nested (this nested task has status = open)
  -[] Nested task with status = completed
    -[x] Completed task
    -[x] Completed task2
  -[ ] Open task
~~~

### Tables

Unimarkup uses grid tables with extended flexibility.

Most notably, columns don't need to align. This helps for easier styling, since some characters are used as keywords, so the table might have more text in Unimarkup, than what is displayed after rendering. A side effect of this is, that `|` must be escaped when used inside a table, even in verbatim and math blocks to get the possibility of multi line rows.

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
~~~
Verbatim block, where nothing is rendered
~~~

~~~~
Outer verbatim block.

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
A render block is used to render graphics, diagrams and charts written in common graph description languages like [mermaid](https://mermaid-js.github.io/) or [opl](https://en.wikipedia.org/wiki/Object_Process_Methodology).
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

### Image insert

Images can be inserted using `![<description>](<image url>)`.

~~~
![<Additional text for this image>](<image url>){<image insert attributes>}
~~~

### File insert

There are two different ways to insert files.

#### Rendered file insert

This way renders the inserted file. There are several supported file types besides unimarkup files.

~~~
"[<Additional text for this file>](<filepath>){<attributes>}
~~~

#### Verbatim file insert

This way inserts the file as is inside a verbatim block. There are several supported file types besides unimarkup files.

~~~
~[<Additional text for this file>](<filepath>){<attributes>}
~~~

### Comments

Unimarkup provides line comments using `****`.

**Note:** It is not possible to have a backslash at the end of a line to get an explicit new line, when a comment is used.

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

### Emojis

Some special character sequences are reserved for direct emoji conversion. Those sequences must be surrounded by whitespaces.

**Some available emojis:**

- `:)` ... 🙂 (U+1F642)
- `;)` ... 😉 (U+1F609)
- `:D` ... 😃 (U+1F603)

~~~
A text with an emoji :D in it!
~~~

Rendered to:
~~~
A text with an emoji 😃 in it!
~~~

The full list of supported emojis can be seen [here](Unimarkup_Language_ReferenceManual.md/##Emojis) 

## Advanced
### Text blocks

~~~
[
  Everything inside is treated as unimarkup text.
  Provided attributes apply to all text inside this block
]{Attributes for the text block}
~~~

### Referencing

There are several possibilities to reference in unimarkup.

#### Footnotes

Footnote content will be rendered at the end of the page before the footer content where the footnote is referenced. If the rendered document is a single page, footnotes are printed at the end of the rendered document. Each footnote has its own unique ID. 

Footnotes are numbered automatically for the rendered output. The numbering scheme can be adapted in the preamble.
It is possible to change between numerical or symbolic numbering and optionally set a header level at which the numbering is reset.

~~~
Referencing a footnote [^^footnote-id]_ [^^myFootnote]_.

_[^^footnote-id] Here is the content of the footnote
_[^^myFootnote] A note
_ can span several
_ lines, but new lines must be added\
_ explicitly by a backslash at the end of a line
_
_ Or with a blank footnote line between 
~~~

#### Endnotes

Endnotes can be used to reference additional content that is only rendered at a specific position in the document.
All used endnotes are rendered using the macro `{@endnotes}`.

Endnotes are numbered automatically for the rendered output. The numbering scheme can be adapted in the preamble.
It is possible to change between numerical or symbolic numbering and optionally set a header level at which the numbering is reset.

~~~
Referencing an endnote [endnote-id^^]_.

Referencing another endnote [note^^]_.

_[endnote-id^^] Here is the content of the endnote
_[note^^] Here is the content of the endnote that
_ can span several
_ lines, but new lines must be added\
_ explicitly by a backslash at the end of a line
_
_ Or with a blank endnote line between 
~~~

#### ID referencing

Every item of an unimarkup document can be referenced by its ID using `[##item-id]_`.

To define the text that is shown when an item is referenced, the attribute `refOption` can be set with the following options

- `headerNumberLvl1` ... shows the number of the header the referenced item is in (The level is from 1 to 6)
- `headerTextLvl1` ... shows the text of the header the referenced item is in (The level is from 1 to 6)
- `label` ... shows the label text of the referenced item
- `prefix` ... shows the prefix text of the referenced item
- `prefixLabel` ... shows the prefix and label text of the referenced item

~~~
![Some image](<image url>){ "ID" : "some-image-ID", "ref" : { "label" : "Some image", "prefix" : "Figure X:" } }

A paragraph that references [##some-image-ID]{ "refOption" : "prefixLabel"}. 
The referenced text looks like: Figure X: Some image 
~~~

#### Literature referencing

Literature references are used to reference books, articles, journals or websites.
To reference a literature, it must be provided via the preamble, JSON or BibTeX file.

To reference a literature, the ID of a literature entry is used and the text that is displayed for this reference is set 
in the form `[&&literature-id{<literature text that is displayed>}]`.

It is possible to reference more than one literature with `[&&first-literature-id{<literature text>}&&second-literature-id{<literature text>}]`.

There are different styles to reference literature entries. Either directly in parentheses, as footnotes or endnotes.
The style must be consistent in the document, so the style is set in the preamble.

To get a list of all used literature references, the macro `{@literature}` can be used. 

~~~
This text has some literature reference [&&literature-id{Author, year}].

This text has more than one literature reference [&&id-1{Author1, year}&&id-2{Author2, year}].


A list of all referenced literature is rendered below:

{@literature}

~~~

### Abbreviations

To use abbreviations inside a text, use `[::<abbreviation>]_`. The full text of an abbreviation can then be displayed as tooltip, inserted instead of the abbreviation, or combined to a list of abbreviations depending on the output format and its options.

Abbreviations must be defined using `_[::<abbreviation>] <full text of the abbreviation>` and surrounded by blank lines, or by other abbreviation definitions. It is possible to span multiple lines by starting the following line with `_ <continuing text>`.

It is possible to render a list of all abbreviations used inside a document using the macro `{@abbr}`.

~~~
Some text using an [::abbr]_. 
~~~

Defining abbreviations:
~~~
_[::abbr] Abbreviation

_[::xml] Extensible Markup Language
_[::html] Hypertext Markup Language
~~~

Multi-word abbreviations are also allowed
~~~
_[::OPC UA TSN] OPC Unified Architecture Time-Sensitive Networking
~~~

Multiple lines are also possible
~~~
_[::mult] Abbreviation
_ spanning multiple lines\
_ Backslash at end creates a rendered new line!
~~~

### Attribute blocks

Attributes are given in JSON-Format. There are default attributes for all unimarkup elements and some specific ones for certain elements.

The list of default attributes can be found [here](Unimarkup_Language_ReferenceManuel.md/##Default-Attributes)

~~~
{Attribute options}
~~~

### Quotation blocks

~~~
> Block quote
> with new lines
> treated as spaces
> as with normal paragraphs
> and other unimarkup syntax is also possible 
>
> > Nested block quote\
> > A backslash at the end of a line creates a new line. 
~~~

### Line blocks

~~~
| Text where *spaces* are preserved as is.
|    All other **markup** however, is considered as **unimarkup text**.
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

### Direct Unicode

~~~
<U+1F642>
~~~

## Dynamics
### Flags

Flags provide the possibility to control the rendered output. Flags are set in the preamble and can be used on text or attribute blocks.

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

### Macros

A macro name can not start with `__`, since it is reserved for internal macros.

~~~
A text that uses {@myMacro}.

This text{@sup{Is superscripted}}
~~~

### Internationalization and localization

Using the attribute block, it is possible to specify identifiers to blocks of text explicitly. Otherwise, identifiers are added implicitly by unimarkup. Every text is then stored in a table with its identifier. New languages can be added, by adding the translated texts into a new column.

