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

Below is only a short overview of the unimarkup language, the full specification can be found in the [Unimarkup language reference manual](Unimarkup_Language_ReferenceManual.md).

## Headers

Headers are in atx-style only with support for 6 heading-levels. For more details, see [LRM-Headers](Unimarkup_Language_ReferenceManual.md#Headers). A header must have an empty new line before and after it, or another header. Header attributes are set at the end of the header text.

**Note:** A header text can have any item that is allowed inside a paragraph.

**Example:**

~~~
# First Main Header

Some unimarkup text for this header...

## Nested Header

More unimarkup text for the nested header...

# Second Main Header
## Other Nested Header

Even more unimarkup text...

# Header with attributes {<header attributes>}

# Multiline
header is also possible

The first paragraph of this header level starts here.

# Multiline
header with
additional attributes {<header attributes>}

# Header with explicit identifier { "id" : "explicit-header-id" }
~~~

## Paragraph items

The following items can be used inside a paragraph.

### Inline formatting

Inline formatting can be used for parts of one paragraph. For multi-paragraph formatting see [text blocks](#text-blocks). 

A non-space character must immediately follow an opened inline formatting. If the inline formatting is not closed by the same character sequence with a non-space character before the closing sequence, no formatting is applied.

**Note:** Inline formatting can also be applied inside words and stacked.

#### Inline formatting items

- **Bold**

  A text is bold by surrounding it with `**`.

  ~~~
  **bold text**
  ~~~

- **Italic**

  A text is italic by surrounding it with `*`.

  ~~~
  *italic text*
  ~~~

- **Underline**

  A text is underlined by surrounding it with `__`.

  ~~~
  __underlined text__
  ~~~

- **Overline**

  A text is overlined by surrounding it with `^_`.

  ~~~
  ^_overlined text^_
  ~~~

- **Strike through**

  A text is strike through by surrounding it with `~~`.

  ~~~
  ~~strike through text~~
  ~~~

- **Superscript**

  A text is superscripted by surrounding it with `^`.

  ~~~
  ^superscripted text^
  ~~~

- **Subscript**

  A text is subscripted by surrounding it with `_`.

  ~~~
  _subscripted text_
  ~~~

- **Verbatim**

  A text can be defined verbatim by surrounding it with `` ` ``.
  If you want to use a `` ` `` inside, you need to use ` `` ` at start and end.

  ~~~
  `verbatim text`

  `` ` ``
  ~~~

- **Highlight**

  A text can be highlighted by surrounding it with `|`.

  ~~~
  |highlighted text|
  ~~~

- **Quote**

  A text can be quoted by surrounding it with `""""`.

  ~~~
  ""quoted text""
  ~~~

#### Inline formatting within words

Inline formatting is possible within words. 

~~~
For*matt*ing inside __word__s is possible.
~~~

#### Stacking inline formatting

Stack inline formatting by nesting them.

~~~
Stacking this **__text to be bold and underlined__**.
The opposite way __**is also bold and underlined**__.
To get ***bold and italic***.
Having a **`bold verbatim text`**.
~~~

### Inline math

  Inline math mode can be used by surrounding formulas with `$`.

  ~~~
  $\frac{1}{n}$
  ~~~

### Inline text group

  Text inside one paragraph can be grouped by surrounding it with `[]`. Only paragraph items can be used inside a text group.
  
  A text group can be used to apply [text attributes](Unimarkup_Language_ReferenceManual.md#text-attributes).

  ~~~
  A paragraph with [grouped text]{ "size" : "20pt" }. Also grouping within one w[or]{ "color" : "rgb(255,0,0)" }d is possible.
  ~~~

### Hyperlinks

Hyperlinks can be set to external sources or IDs. For IDs, the given URL must start with a `#` followed by the ID.

It is possible to set a link title using the `"title"` attribute. If it is not set, the URL is shown.

**Note:** Hyperlinks with IDs as sources should only be used, if an explicit text is wanted. Otherwise, [ID referencing](#id-referencing) should be used.

~~~
[Text represented as hyperlink](url){<optional hyperlink attributes>}

[Explicit hyperlink text for some item](#item-id)

[Hyperlink with an explicit title](some-url){ "title" : "Explicit hyperlink title" }
~~~

### Inline image insert

Images can be inserted inside a paragraph using `![<alternativ text>](<image url>)`.

~~~
Some paragraph text with ![some image](<image url>).

![<Alternativ text for this image>](<image url>){<image insert attributes>}
~~~

### Inline file insert

There are two different ways to insert files inside a paragraph. Optionally it is possible to insert parts of a document with slicing.

**Note:** If the inserted content does not fit inside a paragraph, no content is inserted.

#### Rendered inline file insert

This way renders the inserted file. Supported file types that can be rendered are listed in the [Language Reference Manual](Unimarkup_Language_ReferenceManual.md).

The description given inside `[]` is only used as information about the content of the inserted file. The text will not be in the rendered document.

~~~
"[<Description for the file content that is inserted>](<file path>){<attributes>}

"[Header note](Unimarkup_Language_ReferenceManual.md)<>## Headers .*Note:\*\*< .. >{@blankLine}<>
~~~

#### Verbatim inline file insert

This way inserts the text of a file as is like inline verbatim formatting. Every plain text format can be inserted.

The description given inside `[]` is only used as information about the content of the inserted file. The text will not be in the rendered document.

~~~
~[<Description for the file content that is inserted>](<file path>){<attributes>}

Some paragraph text with ~[Some code](someCodeFile.ads)<<package SPARK_Alloc> .. <end SPARK_Alloc;>>.
~~~

#### Inline file insert slicing

Slicing defines parts of a document that are inserted. The slice is set after the closing brace of the file path.

- `<<Start text that is searched> .. <End text that is searched>>`

  A start and end text is given between `<>` that must match positions inside the inserted document and the start position must be before the end position.

  If both texts are matched in the inserted document, only the text between those two positions is inserted including the two matched texts.

- `<<Start text that is searched>> ..>`

  Here, only the start text position is searched for. If it matches to a text in the inserted document, every text after this position is inserted including the matched text.

- `<.. <End text that is searched>>`

  Every text up to the matched end text is inserted. If no text matches, nothing is inserted.

- Excluding text slice

  It is possible to mark a text that must be matched in the inserted document, but is not included.

  To set a text slice as excluded, use `><` instead of `<>` to surround the text slice.

  `<>excluded text slice< .. <included text slice>>`

**Note:** `<>` above does not mark placeholder values. They are used to mark the start and end of a text slice. 

**Note:** Regex is possible for text slices. The available tokens are described in the [LRM](Unimarkup_Language_ReferenceManual.md).

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

The full list of supported emojis can be seen in the [Language Reference Manual](Unimarkup_Language_ReferenceManual.md/#Emojis) 

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
![Some image](<image url>){ "id" : "some-image-id", "ref" : { "label" : "Some image", "prefix" : "Figure X:" } }

A paragraph that references [##some-image-id]_{ "refOption" : "prefixLabel"}. 
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

This text has more than one literature reference [&&id-1{Author1 page, year}&&id-2{Author2, year}].

The given literature text [&&id-x{can also be nonsense}], but this is up to the writer.

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

### Direct Unicode

Any Unicode code point can be inserted in unimarkup with `&<Unicode code point>;`. Where the *Unicode code point* is given in the form `U+<HEX value>`.

~~~
&U+1F642;
~~~

## Block items

The following items are treated as blocks.

**Note:** A paragraph is also treated as one block.

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

  - Sub bullet list {<bullet list attributes>}

    Paragraph for this sub bullet list

+ Bullet list with different symbol
  * Sub bullet list with different symbol

* Bullet list with id { "id" : "bullet-list-id" }
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
  a. Sub numbered list with latin symbols {<numbered list attributes>}

1. Numbered list with id { "id" : "numbered-list-id" }
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
3. `[a]` Active task (small `a`)
4. `[/]` Failed task

It is possible to get nested task lists, by setting `-[] <task description>` at the higher level.
The state of the higher task depends on the states of all lower tasks.
If at least one lower task is set to fail, the higher task is set to fail. Otherwise, the higher level task is set to active, if any of the lower tasks is set to active. The higher level task is set to completed, if all lower tasks are completed. If there are no active or failed lower tasks and there is at least one open lower task, the higher task is set to open.

~~~
-[ ] Open task
-[x] Completed task
-[a] Active task that is worked on   
-[/] Failed task
-[] Nested task with status = fail
  -[x] Completed task
  -[x] Another one completed
  -[/] Failed task
  -[a] Active task
  -[ ] Open task
-[] Nested task with status = active
  -[x] Completed task
  -[a] Active task
  -[ ] Open task
-[] Nested task with status = completed
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

### Option lists

A bullet list can become an option list, if `...` is set after a space character in the first line of a bullet list item. Any non-space character must be set between the start of the list and `...`.

The content after `...` is indented to align with all other list items of the option list.
Multiple paragraphs can be set as with bullet lists.

Nested option lists indent the content to the right of `...` by the same length to the right compared to the content of the parent content, as the nested item is indented compared to the parent item.

~~~
- Bullet list ... Gets transformed to an option list
- Possible `option` ... Content is indented to the right, to start at the same position as the content from all other option list items.
- Multiple `-paragraphs` ... As with bullet lists

  Multiple paragraphs are possible.
  But the paragraphs are also indented to the same position.

- Nested ... option list
  + Works ... too
~~~

**Note:** The list remains a bullet list, if `...` does not appear in the first line.

~~~
- Bullet list
  that remains ... a bullet list
~~~

### Tables

Unimarkup uses grid tables with extended flexibility. A table is started by a row definition line with `+` and a combination of `-` or `=` and `+`, where a `+` marks a column separation and `-` or `=` mark the column width. 
A table must be ended by a row definition line with same length as the first one and the table must be surrounded by blank lines. The length is the sum of `-`, `+`, `_`, `=` and spaces within the two outer `+`.

Extended flexibility means, that columns do not need to align. This helps for easier styling, since some characters are used as keywords, so the table might have more text in Unimarkup, than what is displayed after rendering. A side effect of this is, that `|` must be escaped when used inside a table, except in verbatim and math blocks to get the possibility of multi-column rows. Multi-column rows are defined by replacing `+` with `-`. The number of `+` defines the number of `|` that are expected per row.

Header rows are marked by setting `=` instead of `-` in the row description line above the content for all columns. Footer rows are marked by setting `_` instead of `-` in the row description line above the content for all columns.

The column width of one `-` is automatically defined by taking the rendered width of the top left table item and scaling other items according to the line ratio of the column definition lines. The column width of one `-` can be overwritten by the `"column-width"` attribute of the table if needed.

The sum of `-`, `=`, `_`, `+` and spaces between the two outer `+` must be the same for all row definition lines to get the same width of all rows. 

One space instead of `-` marks that no line will be created between two rows, creating a multi-row. The number of `-` and spaces between the two rows must match per column. This means that only adjacent columns of rows can be combined. If all columns are combined to multi-row, the next line can be started with `|`.

For easier alignment options, `:` can be used per column definition having no effect on the width scaling of columns. There are 3 alignment options

- `+:--+` ... left alignment
- `+--:+` ... right alignment
- `+:--:+` ... center alignment

**Note:** Column attributes can not be set on multi-row columns, since they take their style from the column above.

~~~
+--+-+--+
| Top left column of table | 1/2 length | same length as top left |
+-------+

+=+=+
| Header column 1 | Header column 2 |
+-+-+
| Normal column 1 | Normal column 2 |
+---+

+-+-+
| Multi row | row 1 |
+ +-+
| paragraph | row 2 |
+---+

+-+-+
| multi row | also multi row |
| for column1 | for column2 |
+---+

+:-+:-:+-:+
| left alignment with `+:--+` | center alignment with `+:--:+` | right alignment with `+--:+` | 
+_+_+_+
| footer1 | footer2 | footer3 |
+---------+

+-+-+-+
| number of `|` | must match | to create |
+---+-+
| multi column | that gets |
+-+---+
| the combined | columns from the line above |
+-----+

+-{<column1 attributes>}+-{<column2 attributes>}+{<row1 attributes>}
| column1 row1 | column2 row1 |
+-{<overwrite column1 attributes for later columns>}+-+
| column1 row2 | column2 row2 {<column2 row2 attributes>}|
+---+{<table attributes>}
~~~

### Verbatim blocks

A verbatim block is started by 3 or more `~` at the start of a new line and must be surrounded by blank lines.

If a verbatim block must be displayed inside a verbatim block,
the outer block must have at least one `~` more than the inner block.

Verbatim blocks can highlight programming code by setting the programming language in the verbatim block attribute `"language"`. Available languages are listed in the [language reference manual](Unimarkup_Language_ReferenceManual.md/##block-attributes).

~~~~~
~~~
Verbatim block, where nothing is rendered
~~~

~~~~
Outer verbatim block.

~~~
Inner verbatim block.
~~~

~~~~

~~~{<Attributes for the verbatim block>}
Verbatim block with given attributes
~~~

~~~{ "language" : "C" }
int add(int a,  int b) {
  return a + b;
}
~~~
~~~~~

### Render blocks

3 or more `'` at start of a line mark the start and end of a render block. A render block must be surrounded by blank lines.

A render block is used to render graphics, diagrams and charts written in common graph description languages like [mermaid](https://mermaid-js.github.io/) or [opl](https://en.wikipedia.org/wiki/Object_Process_Methodology).\
The language must be provided directly after the last `'` at the start of the render block.

Since OPL by default does not specify styling or referencing options, it is extended in unimarkup with the following additions:

- `is object` to define that the given name is an object
- `is process` to define that the given name is a process
- Attribute block at line end

  This is useful to link an object or process to another graph where it is described in more detail for example. Or to provide additional styling information to color an object or process to show test coverage for example.

**Note:** Render blocks can not be nested.

~~~
'''mermaid
graph TB
    A & B--> C & D
'''

'''opl{<render block attributes>}
Unimarkup is object, informatical and systemic.
Pdf is object, informatical and systemic.
Html is object, informatical and systemic.
Converting is process, informatical and systemic.{ "id" : "main-converting-process" }
Converting consumes Unimarkup.
Converting yields Html and Pdf.
'''
~~~

### Math blocks

Math blocks allow using math mode on block level. Text given inside a math block is treated as one mathematical formula.
A math block is given by `$$$` at start and end and must be surrounded by blank lines.

~~~
Blocked math mode

$$$
x = \frac{3}{4}
$$$

$$$
\sum_{i = 1}^n{i^2}
$$$

$$$
\sum_{i = 1}^{\infty}{i^2}
$$$
~~~

### Figure insert

Images can be inserted as figures using `!!![<alternativ text>](<image url>)`.
A figure insert can not be used inside a paragraph. Use [inline image insert](#inline-image-insert) instead to insert an image inside a paragraph.

A figure insert is a block item, allowing an optional caption paragraph. By default, all figure captions are added to an internal list that can be rendered using the macro `{@figureList}`.

~~~
!!![some image](<image url>).
+++
Image that shows something.
+++

!!![<Alternativ text for this image>](<image url>){<image insert attributes>}
~~~

### Block file insert

There are two different ways to insert files as block items. Optionally it is possible to insert parts of a document with slicing. Block file inserts must be surrounded by blank lines.

Slicing is done in the same way as [slicing for inline file inserts](#inline-file-insert-slicing).

#### Rendered block file insert

This way renders the inserted file. Supported file types that can be rendered are listed in the [Language Reference Manual](Unimarkup_Language_ReferenceManual.md).

The description given inside `[]` is only used as information about the content of the inserted file. The text will not be in the rendered document.

~~~
"""[<Description for the file content that is inserted>](<file path>){<attributes>}

"""[Header description without examples](Unimarkup_Language_ReferenceManual.md)<<## Headers> .. >\*\*Example<>
~~~

#### Verbatim block file insert

This way inserts the text of a file as is like a verbatim block. Every plain text format can be inserted.

The description given inside `[]` is only used as information about the content of the inserted file. The text will not be in the rendered document.

~~~~
~~~[<Description for the file content that is inserted>](<file path>){<attributes>}

~~~[Some code](someCodeFile.ads)<<package SPARK_Alloc> .. <end SPARK_Alloc;>>
~~~~

### Text blocks

A text block can be used to group unimarkup text and set attributes that apply to the text inside the text block. Since a text block can have its own ID, it is easy to group and reference text.

A text block is started by `[[[` with a blank line before and ended with `]]]` followed by a blank line.

For nested text blocks, add at least one `[` to the start and the same number of `]` to the end of the parent block.

**Note:** Text styling is applied to every text inside a text block independent of the item type. To get independent styling per type, see [attribute hierarchy](Unimarkup_Language_ReferenceManual.md#attribute-hierarchy).

~~~~
[[[{<Attributes for the text block>}
Everything inside is treated as unimarkup text.
Provided attributes apply to all text inside this block
]]]

[[[[{ "text" : { "color" : "rgb(255,0,0)" }}
Everything inside the text block gets red text-color.

# Main text block

[[[{ "id" : "main-text-block-content"}
A nested text block
]]]

[[[{ "list_bullet" : { "background" : { "color" : "rgb(0,255,0)" }},
    "list_numbered" : { "background" : { "color" : "rgb(0,0,255)" }}}

- This bullet list has a green background

1. This numbered list has a blue background

- Again green background

This paragraph has the default background.

]]]

]]]]

[[[
Any Unimarkup text can be inside a text block

~~~
Verbatim block inside a text block
~~~

]]]
~~~~

### Attribute blocks

Attributes are given in JSON-Format. There are default attributes for all unimarkup elements and some specific ones for certain elements. The allowed position of attribute blocks can be seen in the attribute section of each item in the [Unimarkup LRM](Unimarkup_Language_ReferenceManual.md).

The list of default attributes can be found in the [Unimarkup LRM](Unimarkup_Language_ReferenceManual.md#Default-attributes).

~~~
{Attribute options}
~~~

### Quotation blocks

Quotation blocks can be used to quote longer text sections. A block is started by starting a new line with `>` followed by one space. Multiple lines can be added by starting them with `>` followed by one space. A quotation block must be surrounded by blank lines.

It is possible to use all unimarkup items inside a block quote, but headings are not considered as headers of the document. Styling for quoted headers can be set under the quotation block attribute `"header-styles"` for each level `"lvl<header level>"`.

Quotation blocks can be nested, by setting `>` followed by one space at a new line of a quotation block. Empty quotation lines or blank lines must surround the nested block.

An author text can optionally be set at the end of a quotation block by starting a new line with `>--` followed by one space after an empty quotation line. To get multiple author text lines, start each with `>--`.

~~~
> Block quote
> with new lines
> *treated* as spaces
> as with normal paragraphs
> and other **inline formatting** syntax is also possible 
>
> > Nested block quote\
> > A backslash at the end of a line creates a new line.
> >
> >-- Author
>
>{<Quotation block attributes>}

> Some quoted text
>
>-- by someone
>-- and many others
>--{<Quotation block author attributes>}
~~~

### Line blocks

Line blocks preserve all spaces, tabs and new lines. A line block is started with `|` per new line followed by one space. A block must be surrounded by blank lines.

It is possible to use all unimarkup items inside line blocks, except other line blocks.

**Note:** There is no nesting for line blocks.

**Note:** Since keywords are removed in the rendered document, the text might not align the same way in the raw and rendered form.

**Note:** Setting explicit new lines with a backslash at the end has no effect, since new lines are preserved in line blocks. 

~~~
| Text where *spaces* are preserved as is.
|    All other **markup** however, is considered as **unimarkup text**.

| A verbatim block can be used inside a line block
|
| ~~~
| Some verbatim text
| ~~~
|
| Since spaces are already kept, a verbatim block inside a line block
| is only necessary to get code highlighting.
|{<Line block attributes>}
~~~

### Definition blocks

Definition blocks can be used to set a term with an optional classifier and a definition for this term. A definition block can be useful for theorems or variables.

A definition block is started with `:` per new line followed by one space. A block must be surrounded by blank lines.

The definition block starts with the term. A term can have multiple paragraphs and every Unimarkup item that can be used inside a paragraph. Other Unimarkup items are not allowed. To end the term section, `:` must be set at the end of the last line of the term section. An empty definition line must follow the term section if no classifier is given.

An optional classifier can be set by starting the lines after the term section with `:--`.
Lists are allowed for the classifier besides the supported Unimarkup items in the term section. A blank definition line must follow the classifier.

The definition section allows any Unimarkup item.

~~~
: Definition term :
:
: Definition of this term
: can span multiple lines

: New definition term :
:-- Classifier for this term
:
: Paragraph 1
:
: Paragraph 2

: New term
: spanning several lines :
:-- Also classifiers
:-- can span multiple lines
:
: Paragraph for this term definition

: Main term :{<Term attributes>}
:
: Paragraph for the main term definition.
:
: : Sub term :
: :-- - Classifier with a bullet list
: :-- - Second bullet list item
: :--{<Classifier attributes>}
: :
: : Paragraph for the sub term definition
:
: Other paragraph for the main term definition
:{<Definition block attributes>}
~~~

### Column blocks

There are two ways to create column blocks in unimarkup. 

#### Explicit column blocks

Columns with unimarkup content can be created explicitly by setting 3 or more `|` at the start of a new line with a blank line before the block start and after the block end.

A new column is created using the [new page](#new-page) syntax. Therefore, a new page can not be created inside an explicit column block.

The column orientation can be set using the attribute `"orientation"` with options

- `"leftToRight"` ... The content from top to bottom is oriented **from left to right**
- `"rightToLeft"` ... The content from top to bottom is oriented **from right to left**

Nested explicit column blocks are possible by adding at least one more `|` to the parent block.

~~~
|||
This content is part of the **first** column.

:::

This content is part of the **second** column

:::

This content is part of the **third** column
|||

|||{ "orientation" : "rightToLeft" }
First column is on the most right.

:::

This column is to the left side of the first column

|||

|||{<attributes for the explicit column block>}
{<attributes for column 1>}

Column 1 content

:::{<attributes for column 2>}

Column 2 content

|||

||||
Some content.

:::

|||
Nested column block

:::

Second column of the nested column block
|||

||||
~~~

#### Implicit column blocks

An implicit column block automatically splits its content by a given number of columns. The block is started with `||<number of columns>||` and ended with `||#||`. A blank line must be before the start and end of a block. In contrast to [explicit column blocks](#explicit-column-blocks), all columns have the same width which can not be changed with attributes and the [new page](#new-page) syntax creates a new page.

The content distribution can be defined with the attribute `"distribution"` and options

- `"even"` ... The content is evenly distributed over all columns
- `"page"` ... The content starts in the first column and wraps to the next column at a new page, which is either set explicitly or due to the rendered output
- `"height"` ... The content starts in the first column and wraps to the next column after reaching the column block height

As with the [explicit column blocks](#explicit-column-blocks), the orientation can be set using the `"orientation"` attribute.

To create nested implicit column blocks, add at least one more `|` to both sides of the parent start and end block.

~~~
||<number of columns>||{<implicit column block attributes>}
content that is evenly distributed over the given columns
||#||

||2|| 
This content can have any form of unimarkup content. It is automatically split into two columns.

# Header

- Bullet list
- Inside a column block

# Header2

Some *more* text.
||#||

||3||{ "distribution" : "page" }
This content is in column 1.

Up until a new page is reached.
A new page can be set explicitly

:::

Content in column 2.

A new page can also occur, if the output format is restricted to a certain page size and there is too much content to fit on one page.

`page` and `height` distribution might not fill all columns. The remaining columns will remain blank.
||#||

|||2|||
It is possible to add nested columns

||3||
This content is inside a nested column block.
||#||

|||#|||
~~~

## Other items
### Block titles

A title can be set for a block item by directly preceding the block with one paragraph surrounded by `===`.
A blank line must be set before a block title.

~~~
===
Title for a table
===
+-+-+
| table | row |
+-+-+

===
Another title for a numbered list
===
1. Numbered list
1. Some list
~~~

### Caption

It is possible to set a caption at the end of a block item. A caption can only have one paragraph.
To set a caption to a block, set `+++` on a new line immediately after the block end. To close the caption, set `+++` at the next new line. A blank line must follow a caption.

~~~
!!![figure insert](image.png)
+++
Caption of a figure
+++

+-+-+
| some table | with columns |
+---+
+++
Caption of a table
+++
~~~

### Horizontal line

Set `-` 3 or more times on a new line that is surrounded by blank lines to create a horizontal line.

~~~
---

Another horizontal line after this text.

---
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

At least 3 `:` at start of a line surrounded by blank lines set a new page. How a new page is handled can be set in the preamble.

It is possible to set styling attributes for Unimarkup types like tables, lists or paragraphs that apply only to the following page. See [attribute hierarchy](Unimarkup_Language_ReferenceManual.md#attribute-hierarchy) for more information on how to set attributes for different types.

**Note:** A new page inside an [explicit column block](#explicit-column-blocks) creates a new column instead of a new page.

~~~
:::

:::{<new page with attributes>}

:::{ "text" : { "font" : ["sans serif"] },
  "class" : ["special-page"],
  "table" : { "font" : ["monospace"] }
}

Every text on this page has a *sans-serif* font. Additional styling might be given by the `class` attribute. Tables have a *monospace* font.

:::

This text has the default font again.
~~~

### Preamble

It is possible to define a preamble at the start of a file.

~~~
***
file preamble
***

~~~

### Flags

Flags provide the possibility to control the rendered output. Flags are set in the preamble and can be used on inline text groups, text blocks or attribute blocks.

Since flags represent a boolean condition, it is possible to combine several flags using boolean logic. The logical formula is entered between the two `?`.

**Logical operations with flags:**

- **OR** ... `?flag1 | flag2?` means (flag1 OR flag2)
- **AND** ... `?flag1 & flag2?` means (flag1 AND flag2) 
- **NOT** ... `? !flag1 ?` means (NOT flag1)
- **Precedence** ... `?(flag1 & flag2) | flag3?` means (Either flag1 AND flag2, OR flag3)

~~~
[?flag1? Inline text group that gets rendered, if flag1 is set]
{?flag1? Attributes that are applied, if flag1 is set}

[?flag1 | (!flag2 & flag3)? Inline text group with logical formula]

[[[?flag?
Text block that is rendered, if the flag is set.
]]]
~~~

### Macros

A macro name can not start with `__`, since it is reserved for internal macros.

~~~
A text that uses {@myMacro}.

This text{@sup{Is superscripted}}
~~~

# Internationalization and localization

Using the attribute block, it is possible to specify identifiers to blocks of text explicitly. Otherwise, identifiers are added implicitly by unimarkup. Every text is then stored in a table with its identifier. New languages can be added, by adding the translated texts into a new column.

