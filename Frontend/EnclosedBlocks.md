# Enclosed block elements

Enclosed block elements must be surrounded by blank lines and start and end with special character sequences.
The character sequences must start at the beginning of a new line.
Everything between those character sequences is considered part of the enclosed block.
An optional attribute block may be given directly after the starting character sequence.
The attribute block must start at the same line as the start character sequence, but may span multiple lines.

**Example:**

````
```
verbatim block
```
```` 

**Type:**

: `enclosed-block` :
:-- `Group`
:
: Group type for all enclosed block elements.

## Verbatim blocks

A verbatim block is opened by three or more `` ` `` at the start of a new line and closed with the same number of `` ` `` at a following new line.
The block must be surrounded by blank lines. Content inside a verbatim block is treated as is. No rendering is done and all white-space characters are preserved.
The only exception is a variable of type `text`. The content of a variable of this type is inserted as is inside the verbatim block.
To prevent this, the variable must be escaped with a backslash at any position of the variable.

If a verbatim block must be displayed inside a verbatim block,
the outer block must have at least one `` ` `` more than the inner block.

A highlighter may be set at the start of a verbatim block, by setting the name of an highlighter directly after `` ` ``.
Alternatively, attributes may be set instead of the highlighter name.

**Usage:**

`````
```
Verbatim block, where nothing is rendered
```

````
Outer verbatim block.

```
Inner verbatim block.
```

````

```{<Attributes for the verbatim block>}
Verbatim block with given attributes
```

```C
int add(int a,  int b) {
  return a + b;
}
```
`````

**Type:**

: `verbatim-block` :
:-- `Single`
:
: Element type for verbatim block elements.

**Attributes:**

- [Block attributes](#block-attributes)
- [Text attributes](#text-attributes)

## Render blocks

A render block is opened by three or more `'` at the start of a new line and closed with the same number of `'` at a following new line.
A renderer must be set at the start of a render block, by setting the name of an renderer after the last `'` with optional spaces between.
Attributes may be set after the renderer name. The block must be surrounded by blank lines.
Content inside a render block is rendered depending on the set renderer. See [additional renderer](#additional-renderer) for more information on available renderer.
The only exception is a variable of type `text`. The content of a variable of this type is inserted as is inside the render block.
To prevent this, the variable must be escaped with a backslash at any position of the variable.

**Note:** Render blocks may not be nested.

**Usage:**

```
'''mermaid
graph TB
    A & B--> C & D
'''

'''opl{<render block attributes>}
Unimarkup is informatical and systemic.
Pdf is informatical and systemic.
Html is informatical and systemic.
Converting is informatical and systemic.
Converting consumes Unimarkup.
Converting yields Html and Pdf.
'''
```

**Type:**

: `render-block` :
:-- `Single`
:
: Element type for render block elements.

**Attributes:**

- [Block attributes](#block-attributes)

## Math blocks

Math blocks allow using math mode on block level. Content inside a math block is treated as one mathematical formula.
A math block is opened by three or more `$` at the start of a new line and closed with the same number of `$` at a following new line.
The block must be surrounded by blank lines. Content may be passed inside a math block with a variable of type `text`.
The content of a variable of this type is inserted as is inside the math block.
To use the variable without inserting any content, it must be escaped with a backslash at any position.

By default, all math block [captions](#caption) are added to the list `{%mathCaptions}`.

**Usage:**

```
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
```

**Type:**

: `math-block` :
:-- `Single`
:
: Element type for math block elements.

**Attributes:**

- [Block attributes](#block-attributes)
- [Text attributes](#text-attributes)

## Text block

A text block is opened by three or more `[` at the start of a new line and closed with the same number of `]` at a following new line.
The block must be surrounded by blank lines. For nested text blocks, add at least one `[` to the start and the same number of `]` to the end of the parent block.
The attribute block may be set after the last opening `[`.

Attribute values for every Unimarkup element inside a text block may be set in the attribute block of the text block.
Elements are identified by setting their type name as attribute name.

**Usage:**

````
[[[{<Attributes for the text block>}
Everything inside is treated as Unimarkup content.
Provided attributes apply to all text inside this block
]]]

[[[[{ "heading" : { "color" : "rgb(255,0,0)" }}
# Red main text block

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
Any Unimarkup text may be inside a text block

```
Verbatim block inside a text block
```

]]]
````

**Type:**

: `text-block` :
:-- `Single`
:
: Element type for text block elements.

**Attributes:**

- [Block attributes](#block-attributes)
- [Element attributes](#element-attributes)

## Column blocks

There are two ways to create column blocks in Unimarkup. 

### Explicit column block

Columns with Unimarkup content may be created explicitly by setting 3 or more `|` at the start of a new line with a blank line before the block start and after the block end.
A new column is created using the [page break](#page-break) syntax. Therefore, it is not possible to create a new page inside an explicit column block.

The column orientation may be set using the attribute `"orientation"` with options

- `"leftToRight"` ... The content from top to bottom is oriented **from left to right**
- `"rightToLeft"` ... The content from top to bottom is oriented **from right to left**

Nested explicit column blocks are possible by adding at least one more `|` to the parent block.

**Usage:**

```
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
```

**Type:**

: `explicit-column` :
:-- `Single`
:
: Element type for explicit column elements.

### Implicit column block

An implicit column block automatically splits its content by a given number of columns. The block is started with `|||<number of columns>|` and ended with `|||#|`.
A blank line must be before the start and end of a block. In contrast to [explicit column blocks](#explicit-column-blocks), all columns have the same width which may not be
changed with attributes and the [page break](#page-break) syntax creates a new page.

The content distribution may be defined with the attribute `"distribution"` and options

- `"even"` ... The content is evenly distributed over all columns
- `"page"` ... The content starts in the first column and wraps to the next column at a new page, which is either set explicitly or due to the rendered output
- `"height"` ... The content starts in the first column and wraps to the next column after reaching the column block height

As with the [explicit column blocks](#explicit-column-blocks), the orientation may be set using the `"orientation"` attribute.

To create nested implicit column blocks, add at least one more `|` to the left side of the parent start and end block.

**Usage:**

```
|||<number of columns>|{<implicit column block attributes>}
content that is evenly distributed over the given columns
|||#|

|||2| 
This content may have any form of unimarkup content. It is automatically split into two columns.

# Header

- Bullet list
- Inside a column block

# Header2

Some *more* text.
|||#|

|||3|{ "distribution" : "page" }
This content is in column 1.

Up until a new page is reached.
A new page may be set explicitly

:::

Content in column 2.

A new page may also occur, if the output format is restricted to a certain page size and there is too much content to fit on one page.

`page` and `height` distribution might not fill all columns. The remaining columns will remain blank.
|||#|

||||2|
It is possible to add nested columns

|||3|
This content is inside a nested column block.
|||#|

||||#|
```

**Type:**

: `implicit-column` :
:-- `Single`
:
: Element type for implicit column elements.

## Field block

This element adds a field name at the start of a text block that is enclosed inside `<>`.
This field name may be used for certain output formats or extensions.
If a field name is not known by an output format, or no extension is available to handle the field name, the field block
is treated as a normal [text block](#text-block). Optional flags may be set before the field name. 

**Note:** `<>` is not a placeholder in the usage examples.

**Usage:**

```
[[[<field name>

Any Unimarkup content.

]]]

[[[?someFlag?<someField>

Any Unimarkup content.

]]]
```

**Type:**

: `field-block` :
:-- `Single`
:
: Element type for field block elements.

## Output block

Every content inside an output block is forwarded as is to the rendered document. A block is started with three or more `<` at a new line and ended with the same number of `<` at a following new line.
Output blocks must be surrounded by blank lines and do not allow nesting.

**Usage:**

```
<<<
<script src="someScript.js"></script>
>>>
```

**Type:**

: `output-block` :
:-- `Single`
:
: Element type for output block elements.

## Form block

If form blocks are allowed, predefined form macros may be used next to other Unimarkup content inside a form block to get user input that may be submitted to a URL that is set using the `send-to` attribute.
A form block must be surrounded by blank lines.

**Note:** It is not possible to nest form blocks.

**The following form macros are supported:**

- `{@formText{}}`
- `{@formRadio{}}`
- `{@formSubmit{}}`
- `{@formCheckbox{}}`
- `{@formDate{}}`
- `{@formDatetime{}}`
- `{@formEmail{}}`
- `{@formImage{}}`
- `{@formMonth{}}`
- `{@formNumber{}}`
- `{@formPassword{}}`
- `{@formReset{}}`
- `{@formSearch{}}`
- `{@formTel{}}`
- `{@formTime{}}`
- `{@formUrl{}}`
- `{@formWeek{}}`
- `{@formLabel{}}`
- `{@formSelect{}}`
- `{@formTextarea{}}`
- `{@formSet{}}`

**Usage:**

```
///{ "send-to" : "<some url>"}
**Unimarkup** content may be used like usual!

===
| {@formLabel{First name:}} | {@formText{Sam}}{ "id" : "fname" } |
| {@formLabel{Last name:}} | {@formText{Simpleman}}{ "id" : "lname" } |
===

Radio buttons may flow freely: {@formRadio{%text{Option1}%group{grp1}}}.

===
| {@formSubmit{Press to submit}} | {@formReset{Press to reset}} |
===

Both radio buttons belong together: {@formRadio{%text{Option2}%group{grp1}}}.

{@formSet{%name{Feedback:}%content{
   
  {@formLabel{Write something below}} 
  {@formTextarea{Enter some text...}}

  
  Provide contact information
  
  {@formLabel{Email:}} {@formEmail{sam.simpleman@mail.com}}\
  {@formLabel{Tel:}} {@formTel{}}
}}}

{@formLabel{How do you like Unimarkup so far?}}

<<<
<input type="range" id="happiness" name="happiness" min="0" max="100">
>>>
///
```

**Type:**

: `form-block` :
:-- `Single`
:
: Element type for form block elements.