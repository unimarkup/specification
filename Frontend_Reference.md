# Introduction

This document is the specification for the frontend part of the Unimarkup markup language. 
The frontend part is what the user sees when opening a Unimarkup file inside any plain text editor.

A Unimarkup frontend file has `.um` as an extension.

# Elements

This section contains the element definitions of all Unimarkup elements.

**All elements are grouped in three main element types:**

- [`inline`](#inline-elements)
- [`atomic-block`](#atomic-block-elements)
- [`enclosed-block`](#enclosed-block-elements)

## Inline elements

Inline elements may be part of the content of other elements. They must not contain blank lines themselves.
An optional attribute block may be given at the end of an inline element and may span multiple lines.

**Example:**

~~~
**bold text**, [hyperlink text](url), :D 
~~~

**Type:**

: `inline` :
:-- `Group`
:
: Group type for all inline elements.

### Inline formatting

Inline formatting consists of special character sequences that format an enclosed text in a certain way. For multi-block formatting see [text blocks](#text-blocks).

A none-white-space character must immediately follow an opening character sequence for inline formatting.
If the inline formatting is not closed by the same character sequence with a none-white-space character before the closing character sequence, no formatting is applied.

**Note:** Inline formatting may also be applied inside words and stacked.

**Examples:**

- Inline formatting within words

  ~~~
  For*matt*ing inside __word__s is possible.
  ~~~

- Stacking inline formatting by nesting them

  **Note:** Not all formatting may be combined and some require certain order. Those restrictions are noted at the corresponding formatting definitions.

  ~~~
  Stacking this **__text to be bold and underlined__**.

  The opposite way __**is also bold and underlined**__.

  To get ***bold and italic***.

  Having a **`bold verbatim text`**.

  Combining ^^_overlined superscript^_^ text.
  ~~~

  **Note:** If a special sequence starts inside another one and an closing sequence for an upper formatting is encountered, the inner formatting is not considered, and the outer formatting is closed.

  ~~~
  *outer **only italic*non-bold** non-italic*
  ~~~

  The above renders to the following abstract form

  ~~~
  <italic start>outer **only italic<italic end>non-bold** non-italic*
  ~~~

  **Special cases:**

  - Fallback handling

    Formatting is started at the beginning of an inline content. If a special formatting sequence is reached, it is parsed until another special sequence is encountered.
    The inner sequence is first tried to be completed, but if an end sequence of the outer format is encountered before the inner sequence is completed, the inner is not formatted, and the outer is applied.
    If a formatting is not closed at the end of an inline content, it fails and must not be applied. 

    **Example:**

    ~~~
    *only italic **bold fails* plain text
    ~~~

    The above goes through the following steps:

    1. `<italic start>(only italic <bold start>`
    2. `<italic start<(only italic <bold start>(bold fails* plain text)<end reached>`
    3. `<italic start>(only italic **bold fails)<italic end>`
    4. `<italic start>(only italic **bold fails)<italic end> plain text`

  - Order of `bold` and `italic`

    If `bold` and `italic` are directly stacked, the order depends on the closing sequence.
    Otherwise, `**` is always taken as `bold` and not as opening and/or closing `italic` sequence.

    1. Start and end are stacked

      The order does not matter, since all `*` are part of special sequences and the containing text gets both formats.

      ~~~
      ***bold and italic***
      ~~~

    2. Start is stacked, but `bold` ends before `italic`

      The outer `*` is considered part of `italic` and the inner `**` part of `bold`.

      ~~~
      ***bold and italic** only italic*
      ~~~

    3. Start is stacked, but `italic` ends before `bold`

      The outer `**` is considered part of `bold` and the inner `*` part of `italic`.

      ~~~
      ***bold and italic* only bold**
      ~~~

    4. End is stacked, but `bold` starts before `italic`

      The outer `**` is considered part of `bold` and the inner `*` part of `italic`.

      ~~~
      **only bold *bold and italic***
      ~~~

    5. End is stacked, but `italic` starts before `bold`

      The outer `*` is considered part of `italic` and the inner `**` part of `bold`.

      ~~~
      *only italic **bold and italic***
      ~~~

- No inline formatting

  The following examples show text with formatting character sequences, but no/partial formatting is applied, because not all requirements are fulfilled.

  ~~~
  Text with* starting sequence followed by a white-space.

  Text *with correct starting sequence, but paragraph ends without closing sequence.

  Text *with correct starting sequence, *but ending sequence is preceded by a white-space.

  Text ***with correct bold and italic starting sequence, but* only italic closing sequence is correct with bold being ignored.

  Text ***with correct bold and italic starting sequence, but** only bold closing sequence is correct with italic being ignored.
  ~~~

**Type:**

: `inline_format` :
:-- `Group`
:
: Group type for all inline formatting elements.

#### **Bold**

A text is bold by surrounding it with `**`.

**Usage:**

~~~
**bold text**
~~~

**Type:**

: `inline_format_bold` :
:-- `Single`
:
: Element type for bold inline formatting.

#### **Italic**

A text is italic by surrounding it with `*`.

**Usage:**

~~~
*italic text*
~~~

**Type:**

: `inline_format_italic` :
:-- `Single`
:
: Element type for italic inline formatting.

#### **Underline**

A text is underlined by surrounding it with `__`.

**Usage:**

~~~
__underlined text__
~~~

**Type:**

: `inline_format_underline` :
:-- `Single`
:
: Element type for underline inline formatting.

#### **Overline**

A text is overlined by surrounding it with `^_`.

**Usage:**

~~~
^_overlined text^_
~~~

**Type:**

: `inline_format_overline` :
:-- `Single`
:
: Element type for overline inline formatting.

#### **Strike through**

A text is strike through by surrounding it with `~~`.

**Usage:**

~~~
~~strike through text~~
~~~

**Type:**

: `inline_format_strikethrough` :
:-- `Single`
:
: Element type for strike through inline formatting.

#### **Superscript**

A text is superscripted by surrounding it with `^`.

**Note:** This formatting may not be stacked with subscript formatting.

**Usage:**

~~~
^superscripted text^
~~~

**Type:**

: `inline_format_superscript` :
:-- `Single`
:
: Element type for superscript inline formatting.

#### **Subscript**

A text is subscripted by surrounding it with `_`.

**Note:** This formatting may not be stacked with superscript formatting.

**Usage:**

~~~
_subscripted text_
~~~

**Type:**

: `inline_format_subscript` :
:-- `Single`
:
: Element type for subscript inline formatting.

#### **Verbatim**

A text may be defined as verbatim by surrounding it with `` ` ``.
If you want to use a `` ` `` inside, you need to use ` `` ` instead of `` ` `` with at least one character between the inner content and ` `` `.

**Note:** This formatting must be the most inner formatting for stacked formatting.

**Usage:**

~~~
`verbatim text`

`` ` ``

``char` ``
~~~

**Type:**

: `inline_format_verbatim` :
:-- `Single`
:
: Element type for verbatim inline formatting.

**Attribute:**

: `highlighter` :
:-- Only names of available highlighter are allowed.
:
: The name of the highlighter that should be used.

#### **Highlight**

A text may be highlighted by surrounding it with `||`.

**Usage:**

~~~
||highlighted text||
~~~

**Type:**

: `inline_format_highlight` :
:-- `Single`
:
: Element type for highlight inline formatting.

#### **Quote**

A text may be quoted by surrounding it with `""`.

**Usage:**

~~~
""quoted text""
~~~

**Type:**

: `inline_format_quote` :
:-- `Single`
:
: Element type for quote inline formatting.

### Inline math mode

Inline math mode may be used by surrounding formulas with `$`.
More information about math mode may be found in the [math mode definition section](#math-mode)

**Usage:**

~~~
$\frac{1}{n}$
~~~

**Type:**

: `inline_math` :
:-- `Single`
:
: Element type for inline math mode elements.

**Attributes:**

- [Text attributes](#text-attributes)

### Inline text group

Text inside one paragraph may be grouped by surrounding it with `[]`. Only inline elements may be used inside a text group.
Attributes may be set after the closing `]` of the text group.

**Usage:**

~~~
A paragraph with [grouped text]{ "size" : "20pt" }. Also grouping within one w[or]{ "color" : "rgb(255,0,0)" }d is possible.
~~~

**Type:**

: `inline_textgroup` :
:-- `Single`
:
: Element type for inline text group elements.

**Attributes:**

- [Text attributes](#text-attributes)

### Hyperlink

A hyperlink is set with `[<displayed text>](<link>)`, where the displayed text may only have inline elements.
Hyperlinks may be set to external sources by setting a URL as link, or IDs. For IDs, the given link must start with a `#` followed by the ID.
It is possible to set a link title using the `"title"` attribute. If it is not set, the URL is shown. If no character is set inside `()`, the displayed text is taken as link.
Attributes may be set after the closing `)` of the URL.

Elements of other documents can be linked, by setting `<link to other document>#<element id>` as link.

**Note:** Hyperlinks with IDs as sources should only be used, if an explicit text is wanted. Otherwise, [ID referencing](#id-referencing) should be used.

**Usage:**

~~~
[Text represented as hyperlink](/some/url)

[Explicit hyperlink text for some element](#element-id)

[Hyperlink with an explicit title](some-url){ "title" : "Explicit hyperlink title" }

[https://github.com/]()

[Requirements.md#stick-to-unimarkup]
~~~

**Type:**

: `inline_hyperlink` :
:-- `Single`
:
: Element type for inline hyperlink elements.

**Attributes:**

- [Text attributes](#text-attributes)

: `title` :
:-- `text`
:
: Optional link title that is displayed instead of the URL.

### Inline image

Images may be inserted inside a paragraph using `![<alternate text>](<image url>)`.
The alternate text is shown if the image may not be found, or may be used by screen readers.
It is only possible to use plain text as alternate text.
Optional attributes are set after the closing `)` of the URL.

**Usage:**

~~~
Some paragraph text with ![some image](<image url>).

![<alternate text for this image>](<image url>){<inline image attributes>}
~~~

**Type:**

: `inline_image` :
:-- `Single`
:
: Element type for inline image elements.

**Attributes:**

: `width` :
:-- `unit_size`
:
: Width of the displayed image.

: `height` :
:-- `unit_size`
:
: Height of the displayed image.

: `title` :
:-- `text`
:
: Optional link title that is displayed instead of the URL.

### Inline file insert

There are two different ways to insert files inside a paragraph.
The general form of an inline file insert looks like a hyperlink with a **special character** set before `[`.
Optional attributes are set after the closing `)` of the URL.

**Note:** If the inserted content does not fit inside a paragraph, no content is inserted.

**Note:** The description given inside `[]` is only used as information about the content of the inserted file. The text will not be in the rendered document.

~~~ebnf
inline_insert = hyperlink , [ attribute_block ] ;
~~~

**Type:**

: `inline_insert` :
:-- `Group`
:
: Group type for inline file insert elements.

**Attribute:**

: `insert-id` :
:-- `text`
:
: An ID of a paragraph element of the inserted file may be set, to only include the content of this paragraph,
: even if the file itself would have more content, and could not be inserted as inline. 

#### Rendered inline file insert

Using `'` as special character renders the inserted file depending on the file type.
Supported file types depend on the available renderer. See [additional renderer](#additional-renderer) for more information.

**Usage:**

~~~
'[<description for the file content that is inserted>](<file path>){<attributes>}

'[First heading note](Unimarkup_Language_ReferenceManual.md){ "insert-id" : "first-heading-note" }
~~~

**Type:**

: `inline_insert_rendered` :
:-- `Single`
:
: Element type for inline rendered file insert elements.

**Attribute:**

: `renderer` :
:-- Only names of available renderer are allowed.
:
: The name of the renderer that should be used, if the renderer is not determined automatically from the file type.

#### Verbatim inline file insert

Using `~` as special character inserts the text of a file as is like inline verbatim formatting. Every plain text format may be inserted.
An optional text highlighter may be set as attribute. See [additional highlighter](#additional-highlighter) for more information on available highlighter.

**Usage:**

~~~
~[<description for the file content that is inserted>](<file path>){<attributes>}

Some paragraph text with ~[First heading note](Unimarkup_Language_ReferenceManual.md){ "insert-id" : "first-heading-note" }.
~~~

**Type:**

: `inline-insert-verbatim` :
:-- `Single`
:
: Element type for inline verbatim file insert elements.

**Attribute:**

: `language` :
:-- `text` Default = `plain`
: 
: The name of the markup/programming language that is displayed in the verbatim body.
: Supported languages depend on the used highlighter.

: `highlighter` :
:-- `text` Default = `default`
: 
: The name of the highlighter that should be used.
: Only names of available highlighter are allowed.

### Emoji substitution

Some special character sequences are reserved for direct emoji conversion. Those sequences must be surrounded by white-spaces, or they are kept as is.
It is also possible to use [emoji shortcuts](https://github.com/github/gemoji/blob/master/db/emoji.json) with the alias being surrounded by `:`.
Emoji shortcuts, unlike direct emojis, may appear inside words. The list of supported emoji shortcuts may be increased using the macro `{@<definition> um.addEmoji (%<text>alias%<text>emoji_glyph)}`.

**Full list of available direct emojis:**

- `:)` ... 🙂 (U+1F642) has aliases: `slightly_smiling_face`
- `;)` ... 😉 (U+1F609) has aliases: `wink` 
- `:D` ... 😃 (U+1F603) has aliases: `smiley`
- `^^` ... 😄 (U+1F604) has aliases: `smile`
- `=)` ... 😊 (U+1F60A) has aliases: `blush`
- `:(` ... 🙁 (U+1F641) has aliases: `slightly_frowning_face`
- `;(` ... 😢 (U+1F622) has aliases: `cry`
- `:P` ... 😛 (U+1F61B) has aliases: `stuck_out_tongue`
- `;P` ... 😜 (U+1F61C) has aliases: `stuck_out_tongue_winking_eye`
- `O:)` ... 😇 (U+1F607) has aliases: `innocent`
- `:O` ... 😨 (U+1F628) has aliases: `fearful`
- `>:(` ... 🤬 (U+1F92C) has aliases: `cursing_face`
- `:/` ... 😕 (U+1F615) has aliases: `confused`
- `3:)` ... 😈 (U+1F608) has aliases: `smiling_imp`
- `-_-` ... 😑 (U+1F611) has aliases: `expressionless`
- `<3` ... ❤ (U+2764) has aliases: `heart`
- `(Y)` ... 👍 (U+1F44D) has aliases: `+1`, `thumbsup`
- `(N)` ... 👎 (U+1F44E) has aliases: `-1`, `thumbsdown`

**Usage:**

~~~
{@um.addEmoji (%alias{grin}%emoji_glyph{😁})}
{@um.addEmoji (%alias{slight_smile}%emoji_glyph{&U+1F642;})}

A text with an emoji :D in it!

Using :monocle_face:'s predefined emoji shortcut and the manual :grin: using the macro.

Multiple :grin::grin:
~~~

Rendered to:
~~~
A text with an emoji 😃 in it!

Using 🧐's predefined emoji shortcut and the manual 😁 using the macro.

Multiple 😁😁
~~~

**Type:**

: `inline_emoji` :
:-- `Single`
:
: Type for direct emojis or emoji shortcuts.

### Arrow substitution

Some character sequences are translated to certain Unicode arrows. Those sequences must be surrounded by whitespaces, or they are kept as is.

**Some arrow translations:**

- `-->` ... 🠖 (U+1F816)
- `|-->` ... ↦ (U+21A6)
- `---->` ... ⟶ (U+27F6)
- `|---->` ... ⟼ (U+27FC)
- `==>` ... ⇒ (U+21D2)
- `|==>` ... ⤇ (U+2907)
- `====>` ... ⟹ (U+27F9)
- `|====>` ... ⟾ (U+27FE)
- `<--` ... 🠔 (U+1F814)
- `<--|` ... ↤ (U+21A4)
- `<----` ... ⟵ (U+27F5)
- `<----|` ... ⟻ (U+27FB)
- `<==` ... ⇐ (U+21D0)
- `<==|` ... ⤆ (U+2906)
- `<====` ... ⟸ (U+27F8)
- `<====|` ... ⟽ (U+27F8)
- `<-->` ... ⟷ (U+27F7)
- `<==>` ... ⇔ (U+21D4)

**Usage:**

~~~
A text --> using an arrow!
~~~

Rendered to:

~~~
A text 🠖 using an arrow!
~~~

**Type:**

: `inline_arrow` :
:-- `Single`
:
: Type for arrow translation.

### Referencing

There are several reference variations in Unimarkup.

**Type:**

: `inline_reference` :
:-- `Group`
:
: Group type for reference elements.

#### Notes

Notes may be used to reference additional content that should not be part of the normal document flow.
The `{%um.notes}` list contains all notes that have been referenced up until the current position in the document, where the list is accessed.

A note may be referenced inside a paragraph with `[^^<note-id>]`.

**Note:** The macro [`{@<definition> um.addNote{%id%content}}`](#predefined-macros) must be used to define the note content. 

**Usage:**

~~~
Referencing a note [^^note-id] and [^^myNote].
~~~

**Type:**

: `note-reference` :
:-- `Single`
:
: Element type for referencing defined notes.

#### ID referencing

Every heading and block element of an Unimarkup file may be referenced by its ID using `[##<element-id>]`.
To reference an element that is part of the Unimarkup document, but not in the same Unimarkup file,
the namespace of the Unimarkup file of the element must be set like `[##<namespace>##<element-id>]`.

**Note:** If the element-id contains `##`, it must be escaped to not be considered as namespace.

To define the text that is shown when an element is referenced, the attribute `ref-option` may be used.
Attributes are set after the closing `]`.

**Usage:**

~~~
![Some image](<image url>){ "id" : "some-image-id", "ref" : { "label" : "Some image" } }

A paragraph that references [##some-image-id]{ "refOption" : "label" }. 
The referenced text looks like: Some image
~~~

**Type:**

: `inline_reference_id` :
:-- `Single`
:
: Element type for ID references.

**Attributes:**

- [Text attributes](#text-attributes)

: `ref-option` :
:-- `enum`
:
: This attribute defines the text the reference is substituted with in the rendered document.
:
: Below are the options every heading and block element has:
:
: - `heading-lvl<level number>-nr` ... Shows the number of the heading the referenced element is in (The heading level is from 1 to 6)
: - `heading-lvl<level number>-text` ... Shows the text of the heading the referenced element is in (The heading level is from 1 to 6)
: - `label` ... Shows the label text of the referenced element
:
: The following options are only allowed if the referenced element is a block element:
:
: - `caption` ... Shows the caption paragraph of the referenced block element, if a caption was set
: - `title` ... Shows the title paragraph of the referenced block element, if a title was set

#### Literature referencing

Literature references are used to reference books, articles, journals or websites and use the [Citation Style Language](https://citationstyles.org/) to render literature depending on the provided CSL file.
To reference a literature, the literature meta-data and CSL file must be provided using one of the [configuration options](Configuration_Reference.md).
The literature meta-data must be in a format that is supported by the used CSL processing tool. See the documentation of the used Unimarkup implementation for more information.

A literature is referenced using the ID (called *label* in BibTeX) of a literature entry in the form `[&&<literature-id>]`.
It is possible to reference more than one literature with `[&&<first-literature-id>&&<second-literature-id>]`.

Depending on the used CSL, citations are either `in-text` or `note`. More information may be found in the [CSL specification](https://docs.citationstyles.org/en/1.0.1/specification.html).
In the `note` variant, literature references are treated like [notes](#notes), but references are not added to the note list.
Referenced literatures, used up to the current position in the document, are stored in the list `{%um.usedLiterature}`.

**Note:** If a literature has more than one definition, the behavior depends on the used CSL processor tool.

**Note:** Literature ID restrictions depend on the used CSL processor tool, but must not include `&` and `]`.

**Usage:**

~~~
This text has some literature reference [&&literature-id]
This text has more than one literature reference [&&id-1&&id-2].
~~~

**Type:**

: `inline_reference_literature` :
:-- `Single`
:
: Element type for literature references.

### Abbreviation

Abbreviations may be used as substitution or tooltip with the syntax `[::<abbreviation>]`. The full text of an abbreviation may then be displayed as tooltip or substituted by setting the `display` attribute either to `tooltip` or `substitute`.

**Note:** If an abbreviation is defined more than once, Unimarkup returns and error.

The list `{%um.abbreviations}` holds all used abbreviations in the document up to the current position.

**Usage:**

~~~
Some text using an [::abbr]. 

Text using abbreviations [::xml], [::html] and [::OPC UA TSN].

[::mult]{ "display" : "substitute" }
~~~

**Type:**

: `inline-abbreviation` :
:-- `Single`
:
: Element type for inline abbreviations.

**Attributes:**

: `display` :
:-- `enum`
:
: This attribute defines how the abbreviation definition is displayed.
:
: Possible options are:
:
: - `tooltip` ... The abbreviation definition is shown as tooltip.
:                 **Note:** The tooltip behavior depends on the output format.
: - `substitute` ... This substitutes the abbreviation by the text defined in the definition.

### Direct Unicode

Any Unicode code point may be inserted in Unimarkup with `&<Unicode code point>;`. Where the *Unicode code point* is given in the form `U+<HEX value>`.

**Usage:**

~~~
&U+1F642;
~~~

**Type:**

: `inline_unicode` :
:-- `Single`
:
: Element type for inline Unicode.

### Comment

Unimarkup provides line comments using `;;` to start a comment.
Optionally, a comment can be ended using `;;`, to end a comment before the end of a line. 

**Note:** It is not possible to have a backslash at the end of a line to get an explicit new line, when a comment is used.

**Usage:**

~~~
;; comment to end of line

A comment may be ;; end of line comment
at the end of a line

Comment ;;this is a comment;; inside one line.
~~~

### Inline field

This element adds a field name at the start of an inline text group that is enclosed inside `;`.
This field name may be used for certain output formats or extensions.
If a field name is not known by an output format, or no extension is available to handle the field name, the inline field
is treated as a normal [inline text group](#inline-text-group). Optional flags must be set before the field name. 

**Usage:**

~~~
[;<field name>; Some inline content]

[?someFlag?;someField; Some inline content]
~~~

## Atomic block elements

Atomic block elements must be surrounded by blank lines and must not contain blank lines themselves.
An optional attribute block may be given starting at a new line at the end of an atomic block and may span multiple lines.
None line breaking spaces are allowed before the attribute opening.

**Example:**

~~~
# 1 Heading
## 1.1 Subheading
{ <optional heading attributes for "1.1 Subheading"> }
~~~

**Type:**

: `atomic-block` :
:-- `Group`
:
: Group type for all atomic block elements.

### Heading

Headings are in [atx-style](http://www.aaronsw.com/2002/atx/intro) with support for 6 heading-levels.
A `#` at start of a line followed by a space and a paragraph marks a heading. Adding `#` before the space increases the heading-level. At least one space must be between `#` and the heading text. 

A heading must be surrounded by blank lines, or followed by another heading that is exactly one level lower.
Text after a heading without a blank line is treated as heading text, allowing multiline heading text.
Heading attributes are set at the end of the heading text. 

A heading prefix may be set in the [preamble](#preamble) and may be changed at any point in the document, using the macro `{@setHeadingPrefix{%prefix}}`.
Another overloaded version of this macro may be used to set heading numbering in a more convenient way using `{@setHeadingPrefix{%numbering%startNr%lvlSeparator}}`.
The overloaded macro should only be used before a new level 1 heading is set. The macro `{@renderHeadingNumber}` uses the parameters set in the overloaded macro and may be used to render the heading numbers.

~~~ebnf
heading_end = spaces , none_white_space , paragraph , [ attribut_block ] , blank_line ;

heading_level_1 = blank_line , "#" , heading_end ;
heading_level_2 = blank_line , "##" , heading_end ;
heading_level_3 = blank_line , "###" , heading_end ;
heading_level_4 = blank_line , "####" , heading_end ;
heading_level_5 = blank_line , "#####" , heading_end ;
heading_level_6 = blank_line , "######" , heading_end ;

heading = heading_level_1 | heading_level_2 | heading_level_3 | heading_level_4 | heading_level_5 | heading_level_6 ; 
~~~

**Note:** IDs are created implicitly for headings, by setting Latin characters to lower case, spaces between characters get replaced by `-` and other characters are removed.
If the resulting ID is already present, it must be set explicitly.

**Note:** A heading text may have any element that is allowed inside a paragraph.

**Usage:**

~~~
{@um.setHeadingPrefix(%numbering[roman-upper]%startNr[I])}

# First main heading

Some Unimarkup text for this heading...

## Nested heading

More unimarkup text for the nested heading...

# Second main heading
## Other nested heading

Even more Unimarkup text...
Reference to the first heading [##first-main-heading]

{@um.setHeadingPrefix(%numbering[numeric])}

# Heading with numeric 3 prefixed

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
~~~

**Examples of invalid headings:**

- Wrong heading level of follow-up heading

  ~~~
  # Heading
  # Bad follow-up heading
  ~~~

- No blank lines

  ~~~
  Some text...
  ## No blank lines around heading
  More text...
  ~~~

- No space after `#`

  ~~~
  #No space between # and heading text
  ~~~

**Types:**

: `heading` :
:-- `Group`
:
: Group type for all headings.

: `heading_level_1` :
:-- `Single`
:
: Type for level 1 headings.

: `heading_level_2` :
:-- `Single`
:
: Type for level 2 headings.

: `heading_level_3` :
:-- `Single`
:
: Type for level 3 headings.

: `heading_level_4` :
:-- `Single`
:
: Type for level 4 headings.

: `heading_level_5` :
:-- `Single`
:
: Type for level 5 headings.

: `heading_level_6` :
:-- `Single`
:
: Type for level 6 headings.

**Attributes:**

- [Block attributes](#block-attributes)
- [Text attributes](#text-attributes)

: `show-prefix` :
:-- `bool`
:
: Defines if the heading prefix is shown (`true`), or hidden (`false`).

: `in-toc` :
:-- `bool`
:
: Defines if the heading is added (`true`) to the table of contents, or not (`false`).

### Paragraph

A text starting with at least one none white-space character followed by one or more blank lines is considered as one paragraph. All white-space characters between none white-space characters are replaced by exactly one space.
A backslash `\` at the end of a paragraph line, creates a new line explicitly inside one paragraph.

~~~ebnf
paragraph = blank_line, { any_character } , none_white_space , { any_character } , blank_line ;
~~~

**Usage:**

~~~
This is a paragraph.
New lines, tabs and spaces are treated as one space.

This is a new paragraph.

This is a paragraph\
with an explicit new line.
~~~

**Type:**

: `paragraph` :
:-- `Single`
:
: Type for a paragraph element.
:
: **Note:** Every element of group type `inline` is also of type `paragraph`.

**Note:** A paragraph is part of the `block` type, but without prefix for simplicity.

**Attributes:**

- [Block attributes](#block-attributes)
- [Text attributes](#text-attributes)

### List elements

The following elements are all list elements.
The macro `{@breakLists}` at start of a line between two lists separates those two lists at the highest depth.

- **Nesting lists:**

Text that is indented by $2 * \text{list-depth spaces}$, is part of the list content of this depth.
The main list entry is at depth 1.

**Examples:**

~~~
- Main list entry
  - Two spaces before the list start mark a nested list
    - Another two mark a nested list of a nested list. And so on.
  - This is again only the nested list of the main list

  This text is part of the main list entry

This is some independent paragraph.
~~~

- **Combining lists:**

Lists may be changed at any depth. If the list type changes at the same depth, it is treated as a new list.

**Examples:**

~~~
- Bullet list
  1. Sub numbered list

1. New numbered list
  - Sub bullet list
~~~

**Type:**

: `block_list` :
:-- `Group`
:
: General type for all list elements.

#### **Bullet list**

Any of the characters `-+*` at start of a line followed by a space and any character, is treated as the start of a bullet list.
A list entry heading consists of one paragraph. Indented text at subsequent lines is part of a list entry, but a blank line must be between entry heading and additional entry content.
As an exception, a nested list may directly follow an entry heading. A blank line must follow an additional entry content.
Attributes for list entries are set at the end of the entries heading and bullet list attributes are set at the last list line, but without any spaces before the attribute block.
List entry attributes only apply to the entry heading. If additional content is given, they must be styled in another way. 

~~~ebnf
bullet_list_start_character = "-" | "+" | "*" ;
bullet_list_entry_heading = list_depth_spaces , bullet_list_start_character , space , heading_end ;
bullet_list_entry = bullet_list_entry_heading , line_break , [ ( blank_line , { ( list_depth_spaces , any_character , blank_line ) } ) ] ;

bullet_list = blank_line , bullet_list_entry , { bullet_list_entry } , [ attribute_block ] , blank_line ;
~~~

**Usage:**

~~~~
- Bullet list
  - Sub bullet list

- Other bullet list

  Paragraph for this bullet list

  Other paragraph for this bullet list

  ~~~
  Verbatim block for this bullet list
  ~~~

  - Sub bullet list {<bullet list entry attributes>}

    Paragraph for this sub bullet list

+ Bullet list with different symbol
  * Sub bullet list with different symbol

* Bullet list with id 
  - Sub bullet list indented 2 spaces 
{ "id" : "bullet-list-id" }

Paragraph not for a bullet list

- Bullet list with text
  that spans multiple lines
  but new lines are treated as spaces

{@breakLists}

- Macro above defines this as a new bullet list
~~~~

**Types:**

: `block_list_bullet` :
:-- `Group`
:
: Group type for bullet list elements.
:
: : `block_list_bullet_entry`
: :-- `Single`
: :
: : Element type for a bullet list entry element.

**Attributes:**

- Attributes for the bullet list
  - [Block attributes](#block-attributes)
  - [Text attributes](#text-attributes)

- Attributes for bullet list entries
  -  [Text attributes](#text-attributes)

#### **Numbered list**

Numbered lists have the same behavior as bullet lists, except that enumeration elements are used to start a list entry. Numbered lists also get automatically incremented per new entry in the list
and allow to have the parent number prefixed to the sub list.
If the number is manually increased per entry, no new list is created until the numbering is wrong, at which point a new list is created that starts at this number.

**The following enumerations are allowed:**

- `1.` : Numbered integer list that gets incremented by 1 per new element
- `rI.` : Roman capital character list. Possible characters are `I`, `V`, `X`, `L`, `C`, `D`, `M`
- `Ri.` : Roman lower character list. Possible characters are `i`, `v`, `x`, `l`, `c`, `d`, `m`
- `a.` : Lower Latin character list. After `z`, it goes to `aa`.
- `A.` : Capital Latin character list. After `Z`, it goes to `AA`.

Besides a `.`, it is also possible to use `)`, or surround it like `(1)`, but it must be consistent inside a list.

A parent list entry is prefixed, by concatenating the parent enumeration and the nested enumeration. If the prefixed enumeration is used at a certain level, all other entries at this level must also use the prefixed enumeration.
Otherwise, a new list at this level will be created.

**Usage:**

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
  a. Sub numbered list with latin symbols {<numbered list entry attributes>}

1. Numbered list with id
  1. Sub numbered list indented 2 spaces
{ "id" : "numbered-list-id" }

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
1. doesn't create a new list, but treats it as the paragraph of the element above

(a) Numberbered list
  (a)(a) Sub numbered list with parent number

3. Numbered list starting at specific number
3. Numbered list element that gets incremented automatically
~~~~

**Types:**

: `block_list_numbered` :
:-- `Group`
:
: Group type for numbered list elements.
:
: : `block_list_numbered_entry`
: :-- `Single`
: :
: : Element type for a numbered list entry element.

**Attributes:**

- Attributes for the numbered list
  - [Block attributes](#block-attributes)
  - [Text attributes](#text-attributes)

- Attributes for numbered list entries
  -  [Text attributes](#text-attributes)

#### **Task list**

A task list may be started with `-[<task state>]` followed one space. Additional paragraphs and attributes are set the same way as for bullet lists.
Task lists provide five states to represent tasks.

1. `[ ]` ... Open task (the space between the square brackets is important)
2. `[c]` or `[x]` ... Completed task
3. `[a]` ... Active task
3. `[h]` ... Task on hold
4. `[f]` or `[/]` ... Failed task

It is possible to get nested task lists by setting `-[] <task description>` at the higher level.
The state of the higher task depends on the states of all lower tasks.

The following list is parsed from 1. to 5. to get the higher task state:

1. State = `[/]` (fail): At least one lower task is set to fail
2. State = `[h]` (hold): At least one lower task is set to hold
3. State = `[a]` (active): At least one lower task is set to active
4. State = `[ ]` (open): At least one lower task is set to open
5. State = `[x]` (complete): All lower tasks are set to complete

**Usage:**

~~~
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
~~~

**Types:**

: `block_list_task` :
:-- `Group`
:
: Group type for task list elements.
:
: : `block_list_task_entry`
: :-- `Single`
: :
: : Element type for a task list entry element.

**Attributes:**

- Attributes for the task list
  - [Block attributes](#block-attributes)
  - [Text attributes](#text-attributes)

- Attributes for task list entries
  -  [Text attributes](#text-attributes)

#### **Definition list**

A bullet or numbered list may become a definition list, if `...` is set after a space in a list entry heading. Any none-white-space character must be set between the start of the list entry and `...`.
Multiple paragraphs may be set as with other list elements. The content on the left of `...` is called **definition term** and the content on the right **definition description**.
The option term only allows inline elements. The option description allows all Unimarkup elements.
It is also possible to set a **definition class** directly after `...` by surrounding it with `--`. The definition class only allows inline elements and at least one space must come after the closing `--`.

**Usage:**

~~~
- Bullet list ... Gets transformed to a definition list
- Possible `option` ... Content is indented to the right, to start at the same position as the content from all other definition list elements.
- Multiple `-paragraphs` ... As with bullet lists

  Multiple paragraphs are possible.
  But the paragraphs are also indented to the same position.

- Nested ... definition list
  + Works ... too

- Definition ...--With a class-- And here is the description
~~~

**Note:** The list remains a bullet or numbered list, if `...` does not appear in the list heading entry.

~~~
- Bullet list

  That remains ... a bullet list
~~~

**Types:**

: `block_list_definition` :
:-- `Group`
:
: Group type for definition list elements.
:
: : `block_list_definition_entry`
: :-- `Group`
: :
: : Group type for a definition list entry element.
: :
: : : `block_list_definition_entry_term` :
: : :-- `Single`
: : :
: : : Element type for a definition entry term element.
: : :
: : : `block_list_definition_entry_class` :
: : :-- `Single`
: : :
: : : Element type for a definition entry class element.
: : :
: : : `block_list_definition_entry_description` :
: : :-- `Single`
: : :
: : : Element type for a definition entry description element.

**Attributes:**

- Attributes for the definition list
  - [Block attributes](#block-attributes)
  - [Text attributes](#text-attributes)

- Attributes for definition list entries
  -  [Text attributes](#text-attributes)

### Table

Unimarkup uses grid tables with extended flexibility. A table is started by a row definition line with `+` followed by a combination of table entry specifiers
being `-`, `_`, `=` or spaces and `+`, where a `+` marks a column separation and `-`, `_`, `=` or spaces mark the column width.

**Note:** The first row definition line may not have `_` for all columns or spaces for any column.

Table content is placed between `|` with at least one space difference to a `|`. Each table content row must start and end with one `|`.
A table must be ended by a row definition line that only uses `+` or `-` and the table must be surrounded by blank lines.
This means, that the last line has at least the form `+-+` with additional `+` and `-` added between.

- **Table entry**

  A table entry is identified by the combining the row and column number. Row numbering starts at the top with 1 and increases by one for every new row.
  Column numbering starts at the left with 1 and increases by one for every new column.
  With this numbering, the entry at row=1 column=1 is the top left entry.

  A table entry only allows inline elements and list entry headings of bullet, numbered and task lists.

- **Column width calculation**

  Extended flexibility means that columns do not need to align. This helps for easier styling, since some characters are used as keywords, so the table might have more text in Unimarkup,
  than what is displayed after rendering. A side effect of this is, that `|` must be escaped when used inside a table, except in verbatim and math context, to get the possibility of multi-column rows.

  The rendered width of one `-`, `=` or `_` is automatically defined by taking the rendered width of the top left table element and scaling other elements according to the specifier ratio of the other column definitions.
  The width of a column specifier may be overwritten by the `"column-specifier-width"` attribute of the table if needed.
  Optionally, specifiers may be excluded from this calculation, by encapsulating them inside `()`, but at least one specifier must be set per column.

  **Note:** The number of entry specifiers between the two outer `+`, that are not explicitly excluded, must be the same for all row definition lines to get the same width for all rows.

- **Multi-column multi-row**

  Multi-column rows are defined by replacing `+` with `-`, `=` or `_`. The number of `+` defines the number of `|` that are expected per row.

  One space instead of `-` marks that no line will be created between two rows, creating a multi-row. The number of `-` and spaces between the two rows must match per column.
  This means that only adjacent columns of rows may be combined. If all columns are combined to multi-rows, the next line may directly be started with `|`.

  **Note:** Column attributes may not be set on multi-row columns, since they take their style from the column above.

- **Table header and footer rows**

  Header rows are marked by setting `=` instead of `-` in the row description line above the content for all columns.
  Footer rows are marked by setting `_` instead of `-` in the row description line above the content for all columns.
  Spaces above may also mark header or footer rows, if the previous row is already marked as header or footer.

  **Note:** The table is not rendered, if not all characters per column in a row definition line have the same character.

- **Table header column**

  It is also possible to set header columns by setting `=` or spaces instead of `-` for the column in each row definition line above.
  Spaces are only allowed, if the column was set as a header column before, making it a multi-row header column.

  **Note:** The table is not rendered, if a header column has `-` or `_` in one of its columns in a row definition line.

- **Nested table**

  It is possible to have nested tables, by starting a row definition line inside a table entry.
  The nested table content is then set in the next row definition line of the outer table.
  This requires a multi-column outer table, but the content between the column definitions is not considered for the outer column width.
  Since this shifts the row content of the inner to be one half row lower compared to the outer, the last nested content row must mark the end of the nested table,
  by setting `+-|` at the start and `|-+` at the end of the column entry in the outer row definition line. Setting more `-` between `|` and `+` is possible.
  An optional row attribute of the last nested row may be set between `|` and `-`. The attribute block for the whole nested table may be set between `-` and `+`.
  The inner table is always scaled to fill the column width of the outer table. If the top left entry has a nested table, the rendered width of the top left entry of the nested table is used.

- **Lists inside tables**

  List entry headings of bullet, numbered or task lists may be used inside tables and may be nested and combined using multi-columns.

- **Table attributes**

  Attributes may be set for the whole table, by setting the attribute block at the end of the closing table row.
  Row attributes may be set after the last `|`. Column attributes may be set at the end of the column definition before a `+` inside a row definition line.
  If another column attribute is set for the same column, all columns above have the original column attribute and all further columns get the new one.

- **Horizontal entry alignment**

  For easier horizontal alignment options, `:` may be used at start and end of a column definition, having no effect on the width scaling of columns.
  
  There are 3 alignment options:

  - `+:--+` ... Left alignment
  - `+--:+` ... Right alignment
  - `+:--:+` ... Center alignment

By default, all table [captions](#caption) are added to the list `{%tableCaptions}`.

**Usage:**

~~~
+--+-+--+
| Top left column of table | 1/2 length | same length as top left |
+-------+

+=+=+
| Header column 1 | Header column 2 |
+-+-+
| Normal column 1 | Normal column 2 |
+---+

+=+-+
| Header column | Normal column |
+=+-+
| Header column | Normal column |
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

**Excluding specifiers:**

+-----------------(-------)+--------+
| Some **markup**          | line 1 |
+                 (       )+--------+
| \|\|inside\|\|           | line 2 |
+                 (       )+--------+
| a table                  | line 3 |
+-----------------(-------)+--------+
| normal row               | line 4 |
+-----------------(-------)+--------+

**List inside table:**

+---------------+-------+
| - first       | entry |
+               +-------+
|   - first-sub | entry |
+               +-------+
| - second      | entry |
+---------------+-------+

**Multiline table:**

+---------------------+--------{ "v-alignment" : "center" }+
| paragraph with\     |        |
| explicit new lines\ | center |
| inside a table      |        |
+---------------------+--------{ "v-alignment" : "top" }+
| single row          | row    |
+---------------------+--------+

**Nested table:**

+---------------------------+------+
| +--------+--------------+ | r1c2 |
+ | r1c1.1 | +----------+ | +------+
| +--------+ | r1c1.2.1 | + | r2c2 |
+ | r2c1.1 | +----------+ | +------+
| +--------+-| r2c1.2.1 |-+ | r3c2 |
+-| r3c1.1 |    r3c1.2    |-+------+
~~~

### Figure insert

Images may be inserted as figures using `!!![<alternate text>](<image url>)`.
A figure insert may not be used inside a paragraph. Use [inline image insert](#inline-image-insert) instead to insert an image inside a paragraph.
The alternate text is used if the image may not be found or for screen readers.
Attributes may be set after the closing `)`.

By default, all figure [captions](#caption) are added to the list `{%figureCaptions}`.

**Usage:**

~~~
!!![some image](<image url>).
+++
Image caption that shows something.
+++

!!![<alternate text for this image>](<image url>){<image insert attributes>}
~~~

**Type:**

: `block_figure` :
:-- `Single`
:
: Element type for figure elements.

**Attributes:**

- [Block attributes](#block-attributes)

### Media insert

With media inserts allowed, it is possible to insert video and audio files in addition to images using an extended figure insert syntax that allows to specify multiple sources, in case a media format is not supported, by adding them with `(<alternative source>)` directly after the first source entry.

**Note:** The given sources must all be from the same media type. It is not possible to mix sources for video, media or image types.

**Usage:**

~~~
!!![<Alternative text if media file is not supported>](<media to use>)(<alternative media to use>)

!!![Some video](someVideo.mp4)(someVideo.ogg)(someVideo.webm)
~~~

### Block file insert

There are two different ways to insert files as block elements.
The general form of a block file insert looks like a hyperlink with a **special character** repeated three or more times before `[`.
Block file inserts must be surrounded by blank lines.

**Note:** The description given inside `[]` is only used as information about the content of the inserted file. The text will not be in the rendered document.

**Attributes:**

: `insert-ids` :
:-- `list<text>`
:
: A list of IDs of Unimarkup elements of the inserted file may be set, to only include content of elements with set IDs,
: even if the file itself would have more content. 

: `insert-classes` :
:-- `list<text>`
:
: A list of classes of Unimarkup elements of the inserted file may be set, to only include content of elements,
: that have at least one of those classes set, even if the file itself would have more content.

**Note:** The inserted order of elements depends on the position inside the inserted file.

#### Rendered block file insert

Using `'` as special character renders the inserted file according to its type.
Supported file types depend on the available renderer. If the file type is not supported, nothing is rendered.
See [additional renderer](#additional-renderer) for more information on available renderer.

**Usage:**

~~~
'''[<Description for the file content that is inserted>](<file path>){<attributes>}

'''[The whole style guide for Unimarkup](StyleGuide.md)
~~~

**Type:**

: `block_insert_rendered` :
:-- `Single`
:
: Element type for block rendered file insert elements.

**Attributes:**

- [Block attributes](#block-attributes)

: `renderer` :
:-- Only names of available renderer are allowed.
:
: The name of the renderer that should be used, if the renderer is not determined automatically from the file type.

#### Verbatim block file insert

Using `~` as special character inserts the text of a file as is like a verbatim block. Every plain text format may be inserted.
If no highlighter is available for the inserted file type, the content is inserted as is.
See [additional highlighter](#additional-highlighter) for more information on available highlighter.

**Usage:**

~~~~
~~~[<Description for the file content that is inserted>](<file path>){<attributes>}

~~~[The whole style guide for Unimarkup](StyleGuide.md)
~~~~

**Type:**

: `block_insert_rendered` :
:-- `Single`
:
: Element type for block rendered file insert elements.

**Attributes:**

- [Block attributes](#block-attributes)

: `highlighter` :
:-- Only names of available highlighter are allowed.
:
: The name of the highlighter that should be used, if the highlighter is not determined automatically from the file type.

### Quotation block

Quotation blocks may be used to quote longer text sections. A block is started by starting a new line with `>` followed by one space. Multiple lines may be added by starting them with `>` followed by one space. A quotation block must be surrounded by blank lines.
It is possible to use all Unimarkup elements inside a block quote, but headings are not considered as headings of the document.
Attribute blocks are set at the end of a quotation block.
Like with [text blocks](#text-block), it is possible to set attributes for all Unimarkup elements in the attribute block of a quotation block. 

Quotation blocks may be nested, by setting `>` followed by one space at a new line of a quotation block. Empty quotation lines or blank lines must surround the nested block.

An author text may optionally be set at the end of a quotation block by starting a new line with `>--` followed by one space after an empty quotation line. To get multiple author text lines, start each with `>--`. Only paragraphs may be used for author texts.

**Usage:**

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
>--{<author paragraph attributes>}
~~~

**Type:**

: `block_quote` :
:-- `Single`
:
: Element type for quotation block elements.

**Attributes:**

- [Block attributes](#block-attributes)
- [Element attributes](#element-attributes)

### Line block

Line blocks preserve all spaces, tabs and new lines. A line block is started with `|` per new line followed by one space.
A block must be surrounded by blank lines. It is possible to use all Unimarkup elements inside line blocks, except other line blocks.
Attribute blocks are set at the end of a line block.
Like with [text blocks](#text-block), it is possible to set attributes for all Unimarkup elements in the attribute block of a line block. 

**Note:** There is no nesting for line blocks.

**Note:** Since Unimarkup keywords are removed in the rendered document, the text might not align the same way in the raw and rendered form.

**Note:** Setting explicit new lines with a backslash at the end has no effect, since new lines are preserved in line blocks. 

**Usage:**

~~~
| Text where *spaces* are preserved as is.
|    All other **markup** however, is considered as **Unimarkup text**.

| A verbatim block may be used inside a line block
|
| ~~~
| Some verbatim text
| ~~~
|
| Since spaces are already kept, a verbatim block inside a line block
| is only necessary to get code highlighting.
|{<Line block attributes>}
~~~

**Type:**

: `block_line` :
:-- `Single`
:
: Element type for line block elements.

**Attributes:**

- [Block attributes](#block-attributes)
- [Element attributes](#element-attributes)

### Definition block

Definition blocks may be used to set a term with an optional classifier and a definition for this term.
A definition block is started with `:` per new line followed by one space. A block must be surrounded by blank lines.

The definition block starts with the term. A term may have multiple paragraphs and every Unimarkup element that may be used inside a paragraph.
Other Unimarkup elements are not allowed.
To end the term section, `:` must be set at the end of the last line of the term section.
An empty definition line must follow the term section if no classifier is given.
A term attribute block may be set after the closing `:`.

An optional classifier may be set by starting the lines after the term section with `:--`.
Lists are allowed for the classifier besides the supported Unimarkup elements in the term section.
The last classifier line may contain an attribute block.
A blank definition line must follow the classifier.

The definition section allows any Unimarkup element. Attribute blocks are set at the end of a definition section.
Like with [text blocks](#text-block), it is possible to set attributes for all Unimarkup elements in the attribute block of a definition section. 

**Usage:**

~~~
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
:{<definition block attributes>}
~~~


### Horizontal line

Set `-` 3 or more times on a new line that is surrounded by blank lines to create a horizontal line.

**Usage:**

~~~
---

Another horizontal line after this text.

---
~~~

### Page break

At least 3 `:` at start of a line surrounded by blank lines set a page break. How a page break is rendered depends on the output format.
It is possible to set attributes for Unimarkup elements, but they are only valid until the next page break is set.

**Note:** A page break inside an [explicit column block](#explicit-column-block) creates a new column.

**Usage:**

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

## Enclosed block elements

Enclosed block elements must be surrounded by blank lines and start and end with special character sequences.
The character sequences must start at the beginning of a new line.
Everything between those character sequences is considered part of the enclosed block.
An optional attribute block may be given directly after the starting character sequence.
The attribute block must start at the same line as the start character sequence, but may span multiple lines.

**Example:**

~~~~
~~~
verbatim block
~~~
~~~~  

**Type:**

: `enclosed-block` :
:-- `Group`
:
: Group type for all enclosed block elements.

### Verbatim blocks

A verbatim block is opened by three or more `~` at the start of a new line and closed with the same number of `~` at a following new line.
The block must be surrounded by blank lines. Content inside a verbatim block is treated as is. No rendering is done and all white-space characters are preserved.
The only exception is a variable of type `text`. The content of a variable of this type is inserted as is inside the verbatim block.
To prevent this, the variable must be escaped with a backslash at any position of the variable.

If a verbatim block must be displayed inside a verbatim block,
the outer block must have at least one `~` more than the inner block.

A highlighter may be set at the start of a verbatim block, by setting the name of an highlighter after `~` with optional spaces between.
Attributes may be set after the highlighter name.

**Usage:**

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

~~~ C
int add(int a,  int b) {
  return a + b;
}
~~~
~~~~~

**Type:**

: `block_verbatim` :
:-- `Single`
:
: Element type for verbatim block elements.

**Attributes:**

- [Block attributes](#block-attributes)
- [Text attributes](#text-attributes)

### Render blocks

A render block is opened by three or more `'` at the start of a new line and closed with the same number of `'` at a following new line.
A renderer must be set at the start of a render block, by setting the name of an renderer after the last `'` with optional spaces between.
Attributes may be set after the renderer name. The block must be surrounded by blank lines.
Content inside a render block is rendered depending on the set renderer. See [additional renderer](#additional-renderer) for more information on available renderer.
The only exception is a variable of type `text`. The content of a variable of this type is inserted as is inside the render block.
To prevent this, the variable must be escaped with a backslash at any position of the variable.

**Note:** Render blocks may not be nested.

**Usage:**

~~~
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
~~~

**Type:**

: `block_render` :
:-- `Single`
:
: Element type for render block elements.

**Attributes:**

- [Block attributes](#block-attributes)

### Math blocks

Math blocks allow using math mode on block level. Content inside a math block is treated as one mathematical formula.
A math block is opened by three or more `$` at the start of a new line and closed with the same number of `$` at a following new line.
The block must be surrounded by blank lines. Content may be passed inside a math block with a variable of type `text`.
The content of a variable of this type is inserted as is inside the math block.
To use the variable without inserting any content, it must be escaped with a backslash at any position.

By default, all math block [captions](#caption) are added to the list `{%mathCaptions}`.

**Usage:**

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

**Type:**

: `block_math` :
:-- `Single`
:
: Element type for math block elements.

**Attributes:**

- [Block attributes](#block-attributes)
- [Text attributes](#text-attributes)

### Text block

A text block is opened by three or more `[` at the start of a new line and closed with the same number of `]` at a following new line.
The block must be surrounded by blank lines. For nested text blocks, add at least one `[` to the start and the same number of `]` to the end of the parent block.
The attribute block may be set after the last opening `[`.

Attribute values for every Unimarkup element inside a text block may be set in the attribute block of the text block.
Elements are identified by setting their type name as attribute name.

**Usage:**

~~~~
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

~~~
Verbatim block inside a text block
~~~

]]]
~~~~

**Type:**

: `block_text` :
:-- `Single`
:
: Element type for text block elements.

**Attributes:**

- [Block attributes](#block-attributes)
- [Element attributes](#element-attributes)

### Attribute block

An attribute block is opened with `{` and closed with `}`.
The allowed positions of attribute blocks is defined in the attribute section of each element definition.
The attribute format, attribute groups and hierarchy are described in the [attributes section](#attributes). 

**Usage:**

~~~
## heading {<heading attributes>}

Paragraph text with `**verbatim**`{ "highlighter" : "unimarkup" }
{<paragraph attributes>}
~~~

**Type:**

: `block_attribute` :
:-- `Single`
:
: Element type for attribute block elements.

**Attributes:**

It is possible to concatenate attribute blocks. This allows to use flags for attribute blocks.
If attribute blocks set the same attribute for an element, the last value is taken.

**Example:**

~~~
## heading {?pdf? "color" : "rgb(0,255,0)" }{?html? "color" : "rgb(255,0,0)" }
~~~

### Column blocks

There are two ways to create column blocks in Unimarkup. 

#### Explicit column block

Columns with Unimarkup content may be created explicitly by setting 3 or more `|` at the start of a new line with a blank line before the block start and after the block end.
A new column is created using the [page break](#page-break) syntax. Therefore, it is not possible to create a new page inside an explicit column block.

The column orientation may be set using the attribute `"orientation"` with options

- `"leftToRight"` ... The content from top to bottom is oriented **from left to right**
- `"rightToLeft"` ... The content from top to bottom is oriented **from right to left**

Nested explicit column blocks are possible by adding at least one more `|` to the parent block.

**Usage:**

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

#### Implicit column block

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

~~~
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
~~~


### Field block

This element adds a field name at the start of a text block that is enclosed inside `;`.
This field name may be used for certain output formats or extensions.
If a field name is not known by an output format, or no extension is available to handle the field name, the field block
is treated as a normal [text block](#text-block). Optional flags must be set before the field name. 

**Usage:**

~~~
[[[;<field name>;

Any Unimarkup content.

]]]

[[[?someFlag?;someField;

Any Unimarkup content.

]]]
~~~

### Output block

Every content inside an output block is forwarded as is to the rendered document. A block is started and ended with three or more `<` at a new line.
Output blocks must be surrounded by blank lines and do not allow nesting.

**Usage:**

~~~
<<<
<string>Some important text</strong>
<<<

<<<
<script src="someScript.js"></script>
<<<
~~~

### Form block

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

~~~
///{ "send-to" : "<some url>"}
**Unimarkup** content may be used like always!

+-+-+
| {@formLabel{First name:}} | {@formText{Sam}}{ "id" : "fname" } |
+-+-+
| {@formLabel{Last name:}} | {@formText{Simpleman}}{ "id" : "lname" } |
+---+

Radio buttons may flow freely: {@formRadio{%text{Option1}%group{grp1}}}.

+-+-+
| {@formSubmit{Press to submit}} | {@formReset{Press to reset}} |
+-+-+

Both radio buttons belong together: {@formRadio{%text{Option2}%group{grp1}}}.

{@formSet{%name{Feedback:}%content{
  ===  
  {@formLabel{Write something below}}
  ===
  {@formTextarea{Enter some text...}}

  ===  
  Provide contact information
  ===
  {@formLabel{Email:}} {@formEmail{sam.simpleman@mail.com}}\
  {@formLabel{Tel:}} {@formTel{}}
}}}

{@formLabel{How do you like Unimarkup so far?}}

<<<
<input type="range" id="happiness" name="happiness" min="0" max="100">
<<<
///
~~~

# Element decorations
## Block title

A title may be set for an atomic or enclosed block element by directly preceding the block with one paragraph surrounded by `===`.
A blank line must be set before a block title.

**Usage:**

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

## Caption

It is possible to set a caption at the end of an atomic or enclosed block element. A caption may only have one paragraph.
To set a caption to a block, set `+++` on a new line immediately after the block end. To close the caption, set `+++` at the next new line. A blank line must follow a caption.

**Usage:**

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

# Preamble

It is possible to define a preamble block at the start of a Unimarkup file by surrounding the block with `;;;`
followed by a blank line. Only one preamble is allowed and must start at the first line.

Possible options and alternative configurations ways are defined in the [configuration reference](Configuration_Reference.md).

**Usage:**

~~~
;;;
<preamble>
;;;

~~~

# Escaping special characters

All characters may be escaped using a backslash before them. Escaping characters always means that the escaped character is taken literally.
For example, there is no special meaning for `\n` or `\t`.

**Examples:**

~~~
\\ gets rendered to \
\$ gets rendered to $
\n gets rendered to n
~~~

# Attributes

Attributes are given in [JSON-Format](https://www.json.org/json-en.html).
There are general attributes that are valid for all Unimarkup elements and some specific ones for certain elements.
Default attribute values for all elements may be set in the [preamble](#preamble).

To reset attributes to their default values, write `""` for single value elements, `[]` for arrays and `{}` for objects.
If attributes are not set, default values are used, but resetting may be useful, if some parent changed attribute values that would be inherited.

## General attribute units

Since attributes are defined in JSON-format, there are objects with elements that may have the same attribute units.

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

  Size units are used to define the height or width of an element. A size is given as a decimal value followed by a unit abbreviation (e.g. `16pt`, `1.5em`, `10mm`).
  
  There are two main categories of size units:

  - Absolute units

    - `cm` ... Centimeter
    - `mm` ... Millimeter
    - `in` ... Inch (2.54 cm)
    - `pt` ... Point (1/72 inch)

  - Relative units

    - `em` ... Relative to the font-size of the element (2em = 2 times the size of the current font)
    - `rem` ... Relative to the base font-size of the document
    - `%` ... Relative to the size of the parent element
    
## General attributes

- `"class" : [ "class-name-1", "class-name-2", ... ]`

  Classes that may be used to provide attributes for different elements.

- `"padding" : { }`

  Define the space being added between the content and border of an element using padding.

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

  Define the space being added between the border of an element and the outer frame where other element frames start using margin.

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

  Set a border for an element. 

  - `"radius" : { }`
 
    Border-radius of an element.

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

      Border-color of an element.

    - `"style" : "<border style option>"`

      Border-style with the following options:

      - `none` ... no border
      - `dotted` ... dotted border `......`
      - `dashed` ... dashed border `------`
      - `solid` ... solid border `______`
      - `double` ... double border `======`

    - `"width" : "<size unit>"`

      Border-width of an element.

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

    An image may be set as border.

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

    The background-color of an element.

  - `"image" : [ "<url to image1>", "<url to image2>", ... ]`

    One or more images that are used as backgrounds. Replaces the background-color.

## Text attributes

Text attributes provide attributes for text styling.

- `"font" : ["<font family1>", "<font family2>", ...]`

  Several font families may be set. The first font that is available starting from left is taken. It is also possible to provide generic font family names and a matching available font is then used.

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

  The alignment of a text may have the following values:

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

  This attribute defines the line appearance that may be set for a text like underline, overline and strike through.

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

  `word-break` defines, if a word may be broken at any character at the end of a line (`true`) to prevent an overflow, or if words may't be broken up (`false`).

## Block attributes

- `"id" : "<identifier name>"`
  
  The identifier name must contain at least one character, may not start with a number, and must not contain whitespaces.
  The name is case-sensitive and must be unique in the generated document.
  (The same constraints as with the [HTML ID attribute](https://www.w3schools.com/html/html_id.asp))

  **Note:** If several Unimarkup files are combined, the identifier name must be unique across all.

- `"ref" : { }`
  
  - `"label" : "<paragraph>"`

    The given paragraph may be used when referencing this element.

  - `"prefix" : "<paragraph>"`

    It is possible to set or remove a paragraph for elements, which would be prefixed when referenced.

## Attribute hierarchy

Different attributes may be applied at every level. If there are overlapping attribute values, the most local one is taken.

# Flags

Flags are given in the [preamble](#preamble) and provide the possibility to control the rendered output.
They may be used at the start of inline text groups, text blocks, or attribute blocks by setting `?` directly after the opening character.
Flags may contain any character except `?\&()` and spaces. A second `?` closes the flag section. 

Since flags represent a boolean condition, it is possible to combine several flags using boolean logic.
The logical formula is entered between the two `?`.

**Logical operations with flags:**

- **OR** ... `?flag1 | flag2?` means (flag1 OR flag2)
- **AND** ... `?flag1 & flag2?` means (flag1 AND flag2) 
- **NOT** ... `? !flag1 ?` means (NOT flag1)
- **Precedence** ... `?(flag1 & flag2) | flag3?` means (Either flag1 AND flag2, OR flag3)

**Usage:**

~~~
[?flag1? Text that gets rendered, if flag1 is set]
{?flag1? Attributes that are applied, if flag1 is set}

[?flag1 | (!flag2 & flag3)? Inline text block with logical formula]
~~~

# Macros

Macros may be used to reduce text duplication, improve consistency across documents, or to provide functionality for out of flow elements.
Macros are similar to functions in most common programming languages.

A macro is uniquely identified by a namespace and the macro name. Every macro is inside the namespace of the Unimarkup file in which it is defined.

## Macro definition

A macro may be defined using the following syntax:

- Macro returning inline elements

  ~~~
  ;; Description for this macro
  {@ <return type> macroname (%<parameter type>param1 %<parameter type>param2) => macro body}
  ~~~

  **Note:** The first space after `=>` is mandatory and not considered as part of the body.

- Macro returning block elements

  ~~~
  ;; Description for this macro
  {@ <return type> macroname (%<parameter type>param1 %<parameter type>param2) =>
  macro body
  }
  ~~~

A macro definition is not allowed inside a nested block and may only be surrounded by blank lines or other macro definitions.

**Note:** `<>` are mandatory and no placeholders.

**Note:** If no parameter is set, empty parentheses must be used like `{@<inline> macroname()}`.

**Usage:**

- Defining macros:

  ~~~
  {@<paragraph> macroname(%<paragraph> param1) =>
  Some text: {%param1} (as one paragraph).
  }
  ~~~

- Using macros:

  ~~~
  {@macroname(%param1{using a parameter})}
  ~~~

## Namespaces and macro names

Namespaces may be used to group macros, since `<namespace>.<macro name>` must be unique across the entire document.
Every Unimarkup file has its own namespace, but it is possible to add namespaces inside a file.

A macro name may consist of any character except `{}@.()%<>` and spaces.
If a `.` is part of the name, the text before `.` is considered as a namespace.

Macros defined in the current Unimarkup file may be accessed without a namespace or starting the macro name with `.`.

## Predefined macros

The following macros are predefined and must be part of every Unimarkup implementation.
Predefined macros must have `um` as namespace.

- `{@<text> um.space()}`: This macro adds one non-breaking space
- `{@<text> um.tab()}`: This macro adds two non-breaking spaces






;; mhatzl

- `{@<inline> um.repeat(%<positive> count %<inline> text}}`: This macro repeats a given text for `count` times
- `{@um.defineHeader{all text}}`: This macro defines a header that is applied to a page. It may be overwritten at any point, only the last macro call is taken for the header
- `{@um.defineFooter{all text}}`: This macro defines a footer that is applied to a page. It may be overwritten at any point, only the last macro call is taken for the footer
- `{@um.defineToc}`: This macro inserts the table of contents at this position
- `{@um.defineRefs}`: This macro inserts references used in the document at this position
- `{@um.defineAbbr}`: This macro inserts abbreviations used in the document at this position



# Variables

;; mhatzl

- `{@setCounter{%{word}name%{(no|numeric|roman-upper|roman-lower)}numbering%{natural}startNr%numberingLvl1{{@empty}}%numberingLvl2{{@empty}}%numberingLvl3{{@empty}}%numberingLvl4{{@empty}}%numberingLvl5{{@empty}}%numberingLvl6{{@empty}}}}`

`{@setCounter{%name{headingCnt}%numbering{roman-upper}%startNr{3}}}`

: Possible numbering options are:
:
: - `no` ... No number is prefixed
: - `numeric` ... Numeric values are used
: - `roman-upper` ... Uses upper case roman letters
: - `roman-lower` ... Uses lower case roman letters
:
: If needed, it is possible to define different numbering schemes per level,
: by using `numbering-lvl-<heading level>`. This overwrites the setting of `numbering` for the level.

: `startNr` :
:-- `natural`
:
: Sets the start number for a counter variable.

# Types

;; mhatzl

Unimarkup uses types for all elements. Those types are used for variables and macros,
to define where defined variables and macros are allowed to be used.

**List of all element types:**

- all
- element
- paragraph
- inline
  - formatting
    - inline_bold
    - inline_italic
    - inline_underlined
    - inline_math
    - inline_strikethrough
    - inline_verbatim
  - literature
  - footnote
    - footnote_definition
    - footnote_use
  - endnote
    - endnote_definition
    - endnote_use
  - abbreviation
    - abbreviation_definition
    - abbreviation_use
  - direct_unicode
  - image
  - hyperlink
- heading
- table
  - table_row
  - table_entry
- list
  - list_bullet
  - list_numbered
  - list_task
  - list_definition
- comment
- page_break
- block
  - block_text
  - block_math
  - block_verbatim
  - block_render
  - block_attribute
  - block_quotation
  - block_line
  - block_definition
  - block_figure
- preamble
- number
  - integer
    - natural ... 0 included
    - positive ... 0 not included
    - negative
  - decimal

To combine multiple types except *all*, types may be enclosed in braces and separated by a vertical bar.

~~~
(paragraph|table|block_math)
~~~
