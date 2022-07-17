# Atomic block elements

Atomic block elements must be surrounded by blank lines and must not contain blank lines themselves.
An optional attribute block may be given starting at a new line at the end of an atomic block and may span multiple lines.

**Example:**

```
# 1 Heading
## 1.1 Subheading
{ <optional heading attributes for "1.1 Subheading"> }
```

**Type:**

: `atomic-block` :
:-- `Group`
:
: Group type for all atomic block elements.

## Heading

Headings are in [atx-style](http://www.aaronsw.com/2002/atx/intro) with support for 6 heading-levels.
A `#` at start of a line followed by a space and a paragraph marks a heading. Adding `#` before the space increases the heading-level. At least one space must be between `#` and the heading text. 

A heading must be surrounded by blank lines, or followed by another heading that is exactly one level lower.
Text after a heading without a blank line is treated as heading text, allowing multiline heading text.
Heading attributes are set at the next line after the heading text end. 

A heading prefix may be set using the macro `{@setHeadingPrefix}`.
The macro `{@setNumberedHeadingPrefix}` may be used as an alternative to set heading numbering in a more convenient way.

**Note:** IDs are created implicitly for headings, by setting Latin characters to lower case, spaces between characters get replaced by `-` and other characters
besides numbers are removed.
If the resulting ID is already present, it must be set explicitly to prevent collision.

**Note:** A heading text may have any element that is allowed inside a paragraph.

**Usage:**

```
{@um.setNumberedHeadingPrefix(numbering{roman-upper}, startNr{1})}

# First main heading

Some Unimarkup text for this heading...

## Nested heading

More unimarkup text for the nested heading...

# Second main heading
## Other nested heading

Even more Unimarkup text...
Reference to the first heading [##first-main-heading]

{@um.setNumberedHeadingPrefix(numbering{numeric})}

# Heading with numeric 1 prefixed

# Heading with attributes
{<heading attributes>}

# Multiline
heading is also possible

The first paragraph of this heading level starts here.

# Multiline heading with
additional attributes
{<heading attributes>}

# Heading with explicit identifier
{ "id" : "explicit-heading-id" }
```

**Examples of invalid headings:**

- Wrong heading level of follow-up heading

  ```
  # Heading
  # Bad follow-up heading
  ```

- No blank lines

  ```
  Some text...
  ## No blank lines around heading
  More text...
  ```

- No space after `#`

  ```
  #No space between # and heading text
  ```

**Types:**

: `heading` :
:-- `Group`
:
: Group type for all headings.
: 
: : `heading-level-1` :
: :-- `Single`
: :
: : Type for level 1 headings.
: 
: : `heading-level-2` :
: :-- `Single`
: :
: : Type for level 2 headings.
: 
: : `heading-level-3` :
: :-- `Single`
: :
: : Type for level 3 headings.
: 
: : `heading-level-4` :
: :-- `Single`
: :
: : Type for level 4 headings.
: 
: : `heading-level-5` :
: :-- `Single`
: :
: : Type for level 5 headings.
: 
: : `heading-level-6` :
: :-- `Single`
: :
: : Type for level 6 headings.

**Attributes:**

- [Block attributes](Attributes.md/#block-attributes)
- [Text attributes](Attributes.md/#text-attributes)

: `show-prefix` :
:-- `bool`
:
: Defines if the heading prefix is shown (`true`), or hidden (`false`).
: Default is `true`.

: `in-toc` :
:-- `bool`
:
: Defines if the heading is added (`true`) to the table of contents, or not (`false`).
: Default is `true`.

## Paragraph

A text starting with at least one none white-space character followed by one or more blank lines is considered as one paragraph. All white-space characters between none white-space characters are replaced by exactly one space.
A backslash `\` at the end of a paragraph line, creates a new line explicitly inside one paragraph.

**Usage:**

```
This is a paragraph.
New lines, tabs and spaces are treated as one space.

This is a new paragraph.

This is a paragraph\
with an explicit new line.
```

**Type:**

: `paragraph` :
:-- `Single`
:
: Type for a paragraph element.
:
: **Note:** Every element of group type `inline` is also of type `paragraph`.

**Attributes:**

- [Block attributes](Attributes.md/#block-attributes)
- [Text attributes](Attributes.md/#text-attributes)

## List elements

The following elements are all list elements.
The macro `{@breakLists}` may be used to separate two lists of equal depth.
The depth depends on the placement of the macro. The macro must be on a new line and surrounded by blank lines.

**Type:**

: `list` :
:-- `Group`
:
: General type for all list elements.

- **Nesting lists:**

  Text that is indented by $2 * \text{list-depth spaces}$, is part of the list content of this depth.
  The main list entry is at depth 1.

  **Examples:**

  ```
  - Main list entry
    - Two spaces before the list start mark a nested list
      - Another two mark a nested list of a nested list. And so on.
    - This is again only the nested list of the main list

    This text is part of the main list entry

  This is some independent paragraph.
  ```

- **Combining lists:**

  Lists may be changed at any depth. If the list type changes at the same depth, it is treated as a new list.

  **Examples:**

  ```
  - Bullet list
    1. Sub numbered list

  1. New numbered list
    - Sub bullet list
  ```

- **Setting list attributes:**

  List attributes are set at a new line following the last list entry attributes.
  Since list entry attributes must be set at a new line after the entry content, list attributes cannot be set without setting a list entry attribute.
  To set list attributes without setting list entry attributes, an empty attribute block may be used.

  **Examples:**

  ```
  - list entry
  { <some list entry attributes> }
  { <some list attributes> }

  1. numbered list entry
  {}
  { <some list attributes> }
  ```

### Bullet list

Any of the characters `-+*` at start of a line followed by a space and any none space character, is treated as the start of a bullet list.
`-+*` may be switched freely in a bullet list without creating a new bullet list.
A list entry heading only allows inline elements. Indented text at subsequent lines is part of a list entry,
but a blank line must be between entry heading and additional entry content.
As an exception, a nested list may directly follow an entry heading. A blank line must follow an additional entry content.
Attributes for list entries are set starting at a new line of the entries heading.
List entry attributes only apply to the entry heading. If additional content is given, they must be styled in another way. 

**Usage:**

````
- Bullet list
  - Sub bullet list

- Second main bullet list entry

  Paragraph for this bullet list

  Other paragraph for this bullet list

  ```
  Verbatim block for this bullet list
  ```

  - Sub bullet list
  { <bullet list entry attributes> }

    Paragraph for this sub bullet list

+ Bullet list entry with different symbol
  * Sub bullet list with different symbol

* Bullet list with id
{}
{ "id" : "bullet-list-id" }
  - Sub bullet list indented 2 spaces 

Paragraph not for a bullet list

- Bullet list with text
  that spans multiple lines
  but new lines are treated as spaces

{@breakLists}

- Macro above defines this as a new bullet list
````

**Types:**

: `bullet-list` :
:-- `Group`
:
: Group type for bullet list elements.
:
: : `bullet-list-entry`
: :-- `Single`
: :
: : Element type for a bullet list entry element.

**Attributes:**

- Attributes for the bullet list
  - [Block attributes](Attributes.md/#block-attributes)
  - [Text attributes](Attributes.md/#text-attributes)

- Attributes for bullet list entries
  - [Text attributes](Attributes.md/#text-attributes)

### Numbered list

Numbered lists have the same behavior as bullet lists, except that enumeration elements are used to start a list entry.
Numbered lists also get automatically incremented by 1 per new entry in the list
and allow to have the parent number prefixed to the sub list.
If the number is manually increased per entry, no new list is created until the numbering is wrong, at which point a new list is created that starts at this number.

**The following enumerations are allowed:**

- `1.` : Numbered integer list that gets incremented by 1 per new element
- `rI.` : Roman capital character list. Possible characters are `I`, `V`, `X`, `L`, `C`, `D`, `M`
- `Ri.` : Roman lower character list. Possible characters are `i`, `v`, `x`, `l`, `c`, `d`, `m`
- `a.` : Lower Latin character list. After `z`, it goes to `aa`.
- `A.` : Capital Latin character list. After `Z`, it goes to `AA`.

Besides a `.`, it is also possible to use `)`, or surround it like `(1)`, but it must be consistent inside a list.

A nested numbered list entry is prefixed, by concatenating the parent enumeration and the nested enumeration.
If the prefixed enumeration is used at a certain level, all other entries at this level must also use the prefixed enumeration.
Otherwise, a new list at this level will be created.

**Usage:**

````
1. Start of numbered list
  1. Sub numbered list

1. Second entry in numbered list

  Paragraph for this numbered list

  Other paragraph for this numbered list

  ```
  Verbatim block for this numbered list
  ```

  1. Sub numbered list

    Paragraph for this sub numbered list

rI. Numbered list with capital roman symbols
  rI. Sub numbered list with capital roman symbols

Ri. Numbered list with lower roman symbols
  Ri. Sub numbered list with lower roman symbols

a. Numbered list with latin symbols
  a. Sub numbered list with latin symbols

a. Numbered list with latin symbols
  a. Sub numbered list with latin symbols {<numbered list entry attributes>}

1. Numbered list with id
{}
{ "id" : "numbered-list-id" }
  1. Sub numbered list indented 2 spaces

Paragraph not for a numbered list

1. Numbered list with text
  that spans multiple lines
  but new lines are treated as spaces

{@breakLists}

1. Macro above defines this as new numbered list

1. Numbered list
  1.1. Sub numbered list where the first number is for the parent numbered list
    1.1.1. Sub-sub numbered list
    
      Paragraph for the sub-sub numbered list


1) Numbered list with different style
  1)1) Sub list with parent number
1) Second element of this list
1. doesn't create a new list, but treats it as multiline entry content of the element above

(a) Numberbered list
  (a)(a) Sub numbered list with parent number

3. Numbered list starting at specific number
3. Numbered list element that gets incremented automatically
````

**Types:**

: `numbered-list` :
:-- `Group`
:
: Group type for numbered list elements.
:
: : `numbered-list-entry`
: :-- `Single`
: :
: : Element type for a numbered list entry element.

**Attributes:**

- Attributes for the numbered list
  - [Block attributes](Attributes.md/#block-attributes)
  - [Text attributes](Attributes.md/#text-attributes)

- Attributes for numbered list entries
  - [Text attributes](Attributes.md/#text-attributes)

### Task list

A task list may be started with `-[<task state>]` followed by one space. Additional paragraphs and attributes are set the same way as for bullet lists.
Task lists provide five states to represent tasks.

1. `[ ]` ... Open task (the space between the square brackets is important)
2. `[c]` or `[x]` ... Completed task
3. `[a]` ... Active task
4. `[h]` ... Task on hold
5. `[f]` or `[/]` ... Failed task

It is possible to get nested task lists by setting `-[] <task description>` at the higher level.
The state of the higher task depends on the states of all lower tasks.

The following list is parsed from 1. to 5. to get the higher task state:

1. State = `[/]` (fail): At least one lower task is set to fail
2. State = `[h]` (hold): At least one lower task is set to hold
3. State = `[a]` (active): At least one lower task is set to active
4. State = `[ ]` (open): At least one lower task is set to open
5. State = `[x]` (complete): All lower tasks are set to complete

**Usage:**

```
-[ ] Open task
-[x] Completed task
-[a] Active task that is worked on

  With additional information.

-[/] Failed task
-[] Nested task with status = fail
  -[x] Completed task
  -[x] Another one completed
  -[/] Failed task
  -[a] Active task
  -[ ] Open task
-[] Nested task with status = hold
  -[h] Completed task
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
-[] Nested tasks may be nested (this nested task has status = open)
  -[] Nested task with status = completed
    -[x] Completed task
    -[x] Completed task2
  -[ ] Open task
```

**Types:**

: `task-list` :
:-- `Group`
:
: Group type for task list elements.
:
: : `task-list-entry`
: :-- `Single`
: :
: : Element type for a task list entry element.

**Attributes:**

- Attributes for the task list
  - [Block attributes](Attributes.md/#block-attributes)
  - [Text attributes](Attributes.md/#text-attributes)

- Attributes for task list entries
  - [Text attributes](Attributes.md/#text-attributes)

### Definition list

A bullet or numbered list may become a definition list, if `...` is set after a space in a list entry heading.
Any none-white-space character must be set between the start of the list entry and `...`.
Multiple paragraphs may be set as with other list elements. The content to the left of `...` is called **definition term**,
and the content to the right **definition description**.
Term and description only allow inline elements. However, all Unimarkup elements are allowed for the entry body.
It is also possible to set a **definition class** directly after `...` by surrounding it with `--`.
The definition class only allows inline elements, and at least one space must come after the closing `--`.

**Usage:**

```
- Bullet list ... Gets transformed to a definition list
- Possible `option` ... Content is indented to the right, to start at the same position as the content from all other definition list elements.
- Multiple `-paragraphs` ... As with bullet lists

  Multiple paragraphs are possible.
  But the paragraphs are also indented to the same position.

- Nested ... definition list
  + Works ... too

- Definition ...--With a class-- And here is the description
```

**Note:** The list remains a bullet or numbered list if `...` does not appear in the list heading entry.

```
- Bullet list

  That remains ... a bullet list
```

**Types:**

: `definition-list` :
:-- `Group`
:
: Group type for definition list elements.
:
: : `definition-list-entry`
: :-- `Group`
: :
: : Group type for a definition list entry element.
: :
: : : `definition-list-entry-term` :
: : :-- `Single`
: : :
: : : Element type for a definition entry term element.
: :
: : : `definition-list-entry-class` :
: : :-- `Single`
: : :
: : : Element type for a definition entry class element.
: :
: : : `definition-list-entry-description` :
: : :-- `Single`
: : :
: : : Element type for a definition entry description element.

**Attributes:**

- Attributes for the definition list
  - [Block attributes](Attributes.md/#block-attributes)
  - [Text attributes](Attributes.md/#text-attributes)

- Attributes for definition list entries
  - [Text attributes](Attributes.md/#text-attributes)

## Table

Tables are inspired by [Asciidoctor tables](https://docs.asciidoctor.org/asciidoc/latest/tables/build-a-basic-table/).
A table is started on a newline with three or more `=`, with the possibility to add an explicit table definition,
that is enclosed in parentheses. The closing sequence must be exactly like the opening one.
The table definition provides short variants for commonly used attributes and allows applying individual attributes per column.
Every content row must either start with `|`, or exactly one of `#`, `+` or `_` followed by `|`.
A row must be closed with `|`, followed by optional row attributes.
At least one whitespace must be between `|` and the content of a table entry.
Every new line is treated as a new table row, except tables starting with `+|`, denoting a multi row.
An optional table division may be added with three or more `-`, followed by an optional table division definition that must be enclosed in parentheses.
Heading rows start with `#|` and footer rows with `_|`.

**Note:** Header rows are only allowed before the first normal or footer row.

**Note:** Footer rows are only allowed at the end of a table.

By default, all table [captions](#caption) are added to the list `{%tableCaptions}`.

- **Table entry**

  A table entry is identified by combining the row and column number. Row numbering starts at the top with 1 and increases by one for every new row.
  Column numbering starts at the left with 1 and increases by one for every new column.
  With this numbering, the entry at row=1 column=1 is the top left entry.

  A table entry only allows inline elements and list entry headings of bullet, numbered and task lists.

- **Explicit table definition**

  The table definition allows to set the column width distribution, alignment and attributes.
  It must be enclosed in parentheses and immediately follow the last `=` of the table start.
  Positive numbers may be used to set the distribution ratio per column. The sum of all columns
  must remain constant for all rows of a table. Columns are separated by `,`.
  Column attributes may be used instead of positive numbers.

  - **Alignment options**

    For easier horizontal alignment, `:` may be used in table definitions that use numbers.
    
    There are 3 alignment options:

    - `:<number>` ... Left alignment
    - `<number>:` ... Right alignment
    - `:<number>:` ... Center alignment

    **Usage:**

    ```
    ===(2:, :2, 3, :2:)
    | right aligned | left aligned | default alignment | center aligned |
    ===
    ```

  - **Column header/footer**

    A column may be turned into a header column by surrounding the number with `#`, or into a footer with `_`.

    **Note:** This setting including the number applies to the complete column of the table and cannot be changed in a table division definition.

    **Usage:**

    ```
    ===(#2#, 4, _2_)
    | header column | normal column | footer column |
    | header column | normal column | footer column |
    ===
    ```

- **Table division definition**

  A table division definition is similar to an explicit table definition, but may be set between any two rows that are not merged.
  Three or more `-` followed by positive numbers or column attributes enclosed in parentheses may be used to adapt all further rows.
  Alignment options may be set as defined for the explicit table definition. In addition, it is possible to mark certain columns
  to be merged with the column of the previous row, by using `+`. All columns that should not be merged must be marked with `-`,
  to remain unchanged, or given a positive number or column attribute.

  **Note:** The merged column(s) must remain aligned to the previous column(s) they are merged with.

  **Usage:**

  ```
  ===
  | column 1 | column 2 | column 3 |
  ---(-,+,-)
  | column 1 | merged column 2 | column 3 |
  ===
  ```

- **Column width calculation**

  If no explicit table definition is set, every column is evenly distributed according to the maximum width of the table.
  Otherwise, the ratios between the positive numbers from the definition are used, by summing up all numbers.
  All further table division definitions must keep the same total sum, but may rearrange the numbers.

- **Shorthand table definitions**

  As convenience feature, it is possible to combine several columns either in an explicit table definition or table division definition,
  by setting a positive number followed by `x` before the actual column value, which is either a positive number or column attribute.
  The number given before the `x` is the number of columns that are spanned by the given setting.
  If only a single column setting is given, it applies to all columns without the need to apply a multiplication factor.

**Usage:**

```
===(2:, :2, 3, :2:)
| right aligned | left aligned | spanning | center aligned |
---(-, -, +, -)
| settings kept | settings kept | two rows | settings kept |
---
| settings kept | settings kept | new row | settings kept |
===

===
#| header row |
#| 2nd header row |
| normal row |
_| footer row |
===

===
#| header row |
+| merged header row |
| normal row |
_| footer row |
+| merged footer row |
===

===(#2#, 4, _2_)
| header column | normal column | footer column |
| header column | normal column | footer column |
===

===(2, 4)
| small column | wide column  |
---(4, 2)
| wide column  | small column |
===

===
| merged | merged |
+| rows  | rows   |
===

===
| row 1 | row 1 |
| row 2 | row 2 |
===

===({<column 1 attributes>}, {<column 2 attributes>}, {<column 3 attributes>}){<table attributes>}
| row 1 | row 1 | row 1 |{<row 1 attributes>}
| row 2 | row 2 | row 2 |{<row 2 attributes>}
===

===(2x1, 4)
| small column | small column | wide column  |
---(1, 4, 1)
| small column | wide column  | small column |
===

===(2x{<attributes for column 1 and 2>}, {<column 3 attributes>})
| row 1 | row 1 | row 1 |
| row 2 | row 2 | row 2 |
===

===({<attributes for all columns>})
| row 1 | row 1 | row 1 |
| row 2 | row 2 | row 2 |
===
```

**Type:**

: `table` :
:-- `Single`
:
: Element type for table elements.

## Figure insert

Images may be inserted as figures using `!!![<alternate text>](<image uri> <optional title>)`.
A figure insert may not be used inside a paragraph. Use [inline image insert](Inlines.md/#inline-image-insert) instead to insert an image inside a paragraph.
The alternate text is used if the image may not be found or for screen readers.
An optional link title may be set after the image URI separated by at least one whitespace.
Attributes may be set after the closing `)`.

By default, all figure [captions](#caption) are added to the list `{%figureCaptions}`.

**Usage:**

```
!!![some image](<image uri> myImageTitle).
+++
Image caption.
+++

!!![<alternate text for this image>](<image uri>){<figure insert attributes>}
```

**Type:**

: `figure` :
:-- `Single`
:
: Element type for figure elements.

**Attributes:**

- [Block attributes](Attributes.md/#block-attributes)

## Media insert

With media inserts allowed, it is possible to insert video and audio files in addition to images using an extended figure insert syntax that allows to specify multiple sources, in case a media format is not supported, by adding them with `(<alternative source>)` directly after the first source entry.

**Note:** The given sources must all be from the same media type. It is not possible to mix sources for video, media or image types.

**Note:** A link title may only be set on the first URI and is shared for all sources.

**Usage:**

```
!!![<Alternative text if media file is not supported>](<media to use>)(<alternative media to use>)

!!![Some video](someVideo.mp4)(someVideo.ogg)(someVideo.webm)
```

**Type:**

: `media-insert` :
:-- `Single`
:
: Element type for media insert elements.

## Block file insert

There are two different ways to insert files as block elements.
The general form of a block file insert looks like a hyperlink with a **special character** repeated three times before `[`.
Block file inserts must be surrounded by blank lines.

**Note:** The description given inside `[]` is only used as information about the content of the inserted file. The text will not be in the rendered document.

**Type:**

: `block-insert` :
:-- `Single`
:
: Group type for block insert elements.

**Attributes:**

: `insert-ids` :
:-- `list<text>`
:
: A list of IDs of Unimarkup elements of the inserted file may be set to only include content of elements with set IDs,
: even if the file itself would have more content.

: `insert-classes` :
:-- `list<text>`
:
: A list of classes of Unimarkup elements of the inserted file may be set to only include content of elements
: that have at least one of those classes set, even if the file itself would have more content.

**Note:** The inserted order of elements depends on the position inside the inserted file.

### Rendered block file insert

Using `'` as special character renders the inserted file according to its type.
Supported file types depend on the available renderer. If the file type is not supported, nothing is rendered.
See [additional renderer](#additional-renderer) for more information on available renderer.

**Usage:**

```
'''[<Description for the file content that is inserted>](<file path>){<attributes>}

'''[The whole style guide for Unimarkup](StyleGuide.md)
```

**Type:**

: `rendered-block-insert` :
:-- `Single`
:
: Element type for block rendered file insert elements.

**Attributes:**

- [Block attributes](Attributes.md/#block-attributes)

: `language` :
:-- `text` Default = `plain`
: 
: The name of the language that is displayed in the render body.
: Supported languages depend on the used renderer.
:
: **Note:** If `plain` is set, the renderer may try to guess the language to render.

: `renderer` :
:-- `text` Default = `default`
:
: The name of the renderer that should be used.
: Only names of available renderer are allowed.

### Verbatim block file insert

Using `` ` `` as special character inserts the text of a file as is like a verbatim block. Every plain text format may be inserted.
If no highlighter is available for the inserted file type, the content is inserted as is.
See [additional highlighter](#additional-highlighter) for more information on available highlighter.

**Usage:**

````
```[<Description for the file content that is inserted>](<file path>){<attributes>}

```[The whole style guide for Unimarkup](StyleGuide.md)
````

**Type:**

: `verbatim-block-insert` :
:-- `Single`
:
: Element type for block rendered file insert elements.

**Attributes:**

- [Block attributes](Attributes.md/#block-attributes)

: `language` :
:-- `text` Default = `plain`
: 
: The name of the markup/programming language that is displayed in the verbatim body.
: Supported languages depend on the used highlighter.
:
: **Note:** If `plain` is set, the highlighter may try to guess the language to highlight.

: `highlighter` :
:-- `text` Default = `default`
: 
: The name of the highlighter that should be used.
: Only names of available highlighter are allowed.

## Quotation block

Quotation blocks may be used to quote longer text sections. A block is started by starting a new line with `>` followed by one space.
Multiple lines may be added by starting them with `>` followed by one space. A quotation block must be surrounded by blank lines.
It is possible to use all Unimarkup elements inside a block quote, but headings are not considered as headings of the document.
An attribute block may be set at a new line at the end of a quotation block, and may span multiple lines.
Like with [text blocks](EnclosedBlocks.md/#text-block), it is possible to set attributes for all Unimarkup elements in the attribute block of a quotation block. 

Quotation blocks may be nested, by setting `>` followed by one space at a new line of a quotation block.
Empty quotation lines or blank lines must surround the nested block.

An author text may optionally be set at the end of a quotation block by starting a new line with `>--` followed by one space after an empty quotation line.
To get multiple author text lines, start each with `>--`. Only inline elements may be used for author texts.

**Usage:**

```
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
{<Quotation block attributes>}

> Some quoted text
>
>-- by someone
>-- and many others
>--{<author paragraph attributes>}
```

**Type:**

: `block-quote` :
:-- `Single`
:
: Element type for quotation block elements.

**Attributes:**

- [Block attributes](Attributes.md/#block-attributes)
- [Element attributes](Attributes.md/#element-attributes)

## Line block

Line blocks preserve all spaces, tabs and new lines. A line block is started with `|` per new line followed by one space.
A block must be surrounded by blank lines. It is possible to use all Unimarkup elements inside line blocks, except other line blocks.
An attribute block may be set at a new line at the end of a line block, and may span multiple lines.
Like with [text blocks](EnclosedBlocks.md/#text-block), it is possible to set attributes for all Unimarkup elements in the attribute block of a line block. 

**Note:** There is no nesting for line blocks.

**Note:** Since Unimarkup keywords are removed in the rendered document, the text might not align the same way in the raw and rendered form.

**Note:** Setting explicit new lines with a backslash at the end has no effect, since new lines are preserved in line blocks. 

**Usage:**

```
| Text where *spaces* are preserved as is.
|    All other **markup** however, is considered as **Unimarkup text**.

| A verbatim block may be used inside a line block
|
| ```
| Some verbatim text
| ```
|
| Since spaces are already kept, a verbatim block inside a line block
| is only necessary to get code highlighting and prevent rendering.
{<Line block attributes>}
```

**Type:**

: `line-block` :
:-- `Single`
:
: Element type for line block elements.

**Attributes:**

- [Block attributes](Attributes.md/#block-attributes)
- [Element attributes](Attributes.md/#element-attributes)

## Definition block

Definition blocks may be used to set a term with an optional classifier and a definition for this term.
A definition block is started with `:` per new line followed by one space. A block must be surrounded by blank lines.

The definition block starts with the term. A term only allows inline elements.
To end the term section, `:` must be set at the end of the last line of the term section.
An empty definition line must follow the term section if no classifier is given.
A term attribute block may be set after the closing `:`.

An optional classifier may be set by starting the lines after the term section with `:--`.
Lists are allowed for the classifier besides the supported Unimarkup elements in the term section.
The last classifier line may contain an attribute block.
A blank definition line must follow the classifier.

The definition section allows any Unimarkup element.
An attribute block may be set at a new line at the end of a definition block, and may span multiple lines.
Like with [text blocks](EnclosedBlocks.md/#text-block), it is possible to set attributes for all Unimarkup elements in the attribute block of a definition section. 

**Usage:**

```
: Definition term :
:
: Definition of this term
: may span multiple lines

: New definition term :
:-- Classifier for this term
:
: Paragraph 1
:
: Paragraph 2

: New term
: spanning several lines :
:-- Also classifiers
:-- may span multiple lines
:
: Paragraph for this term definition

: Main term :{<term attributes>}
:
: Paragraph for the main term definition.
:
: : Sub term :
: :-- - Classifier with a bullet list
: :-- - Second bullet list element
: :--{<classifier attributes>}
: :
: : Paragraph for the sub term definition
:
: Other paragraph for the main term definition
{<definition block attributes>}
```

**Type:**

: `definition-block` :
:-- `Group`
:
: Group type for definition blocks.
:
: `definition-block-term` :
:-- `Single`
:
: Element type for definition block term elements.
:
: `definition-block-class` :
:-- `Single`
:
: Element type for definition block class elements.

## Horizontal line

Set `-` 3 or more times on a new line that is surrounded by blank lines to create a horizontal line.

**Usage:**

```
---

Another horizontal line after this text.

---
```

**Type:**

: `horizontal-line` :
:-- `Single`
:
: Element type for horizontal line elements.

## Page break

At least 3 `:` at start of a line surrounded by blank lines set a page break. How a page break is rendered depends on the output format.
It is possible to set attributes for Unimarkup elements, but they are only valid until the next page break is set.

**Note:** A page break inside an [explicit column block](EnclosedBlocks.md/#explicit-column-block) creates a new column.

**Usage:**

```
:::

:::{<new page with attributes>}

:::{ "text" : { "font" : ["sans serif"] },
  "class" : ["special-page"],
  "table" : { "font" : ["monospace"] }
}

Every text on this page has a *sans-serif* font. Additional styling might be given by the `class` attribute. Tables have a *monospace* font.

:::

This text has the default font again.
```

**Type:**

: `page-break` :
:-- `Single`
:
: Element type for page break elements.
