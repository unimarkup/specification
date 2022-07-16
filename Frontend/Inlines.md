# Inline Elements

Inline elements may be part of the content of other elements. They must not contain blank lines themselves.
An optional attribute block may be given at the end of an inline element and may span multiple lines.

**Example:**

```
**bold text**, [hyperlink text](url), :D 
```

**Type:**

: `inline` :
:-- `Group`
:
: Group type for all inline elements.

## Inline formatting

Inline formatting consists of special character sequences that format an enclosed text in a certain way. For multi-block formatting see [text blocks](#text-blocks).

A none-white-space character must immediately follow an opening character sequence for inline formatting.
If the inline formatting is not closed by the same character sequence with a none-white-space character before the closing character sequence, no formatting is applied.

**Note:** Verbatim formatting is an exception and is applied independent of white-space characters.

**Note:** Inline formatting may also be applied inside words and stacked.

**Examples:**

- Inline formatting within words

  ```
  For*matt*ing inside __word__s is possible.
  ```

- Stacking inline formatting by nesting them

  **Note:** Not all formatting may be combined and some require certain order. Those restrictions are noted at the corresponding formatting definitions.

  ```
  Stacking this **__text to be bold and underlined__**.

  The opposite way __**is also bold and underlined**__.

  To get ***bold and italic***.

  Having a **`bold verbatim text`**.

  Combining ^‾overlined superscript‾^ text.
  ```

  **Special cases:**

  - Fallback handling

    Formatting is started at the beginning of an inline content. If a special formatting sequence is reached, it is parsed until another special sequence is encountered.
    The inner sequence is first tried to be completed, but if an end sequence of the outer format is encountered before the inner sequence is completed, the inner is not formatted, and the outer is applied.
    If a formatting is not closed at the end of an inline content, it fails and must not be applied. 

    **Examples:**

    ```
    *outer **only italic*non-bold** non-italic*
    ```

    The above renders to the following abstract form

    ```
    <italic start>outer **only italic<italic end>non-bold** non-italic*
    ```

    ```
    *only italic **bold fails* plain text
    ```

    The above goes through the following steps:

    1. `<italic start>(only italic <bold start>`
    2. `<italic start<(only italic <bold start>(bold fails* plain text)<end reached>`
    3. `<italic start>(only italic **bold fails)<italic end>`
    4. `<italic start>(only italic **bold fails)<italic end> plain text`

  - Order of `bold` and `italic`

    If `bold` and `italic` are directly stacked, the order depends on the closing sequence.
    Otherwise, `**` is always taken as `bold` and not as opening and/or closing `italic` sequence.

    **Note:** The same applies for `subscript` and `underline`.

    1. Start and end are stacked

      The order does not matter, since all `*` are part of special sequences and the containing text gets both formats.

      ```
      ***bold and italic***
      ```

    2. Start is stacked, but `bold` ends before `italic`

      The outer `*` is considered part of `italic` and the inner `**` part of `bold`.

      ```
      ***bold and italic** only italic*
      ```

    3. Start is stacked, but `italic` ends before `bold`

      The outer `**` is considered part of `bold` and the inner `*` part of `italic`.

      ```
      ***bold and italic* only bold**
      ```

    4. End is stacked, but `bold` starts before `italic`

      The outer `**` is considered part of `bold` and the inner `*` part of `italic`.

      ```
      **only bold *bold and italic***
      ```

    5. End is stacked, but `italic` starts before `bold`

      The outer `*` is considered part of `italic` and the inner `**` part of `bold`.

      ```
      *only italic **bold and italic***
      ```

  - Four contiguous `*` or `_`

    **Note:** With contiguous, it is meant that no character of the four is taken as close sequence up until now.

    The following definition is using `*` for `bold` and `italic`,
    but the same manner applies for `_` and `subscript` and `underline`.

    The leftmost `*` is taken as plain text and the remaining three are taken as combined open.
    If open is not allowed due to open constraints, those three `*` are also taken as plain.

    ```
    ****bold and italic***
    ```

    The above renders to

    ```
    *<combined start>bold and italic<combined end>
    ```

  - Four none-contiguous `*` or `_`

    Here, the rendered result depends on previous open sequences.
    The following definition is using `*` for `bold` and `italic`,
    but the same manner applies for `_` and `subscript` and `underline`.

    If no whitespace is before the leftmost `*`, then the characters are used as closing sequences
    for bold, italic and combined. The remaining characters are then used as open sequences respectively.

    **Note:** Two consecutive sequences are always treated as `bold`.

    ```
    ***bold and italic****italic*
    ```

    The above renders to

    ```
    *<combined start>bold and italic<combined end><italic start>italic<italic end>
    ```

    **Note:** The above could be written as `***bold and italic**italic*`.


- No inline formatting

  The following examples show text with formatting character sequences, but no/partial formatting is applied, because not all requirements are fulfilled.

  ```
  Text with* starting sequence followed by a white-space.

  Text *with correct starting sequence, but paragraph ends without closing sequence.

  Text *with correct starting sequence, *but ending sequence is preceded by a white-space.

  Text ***with correct bold and italic starting sequence, but* only italic closing sequence is correct with bold being ignored.

  Text ***with correct bold and italic starting sequence, but** only bold closing sequence is correct with italic being ignored.
  ```

**Type:**

: `inline-format` :
:-- `Group`
:
: Group type for all inline formatting elements.

### Bold

A text is bold by surrounding it with `**`.

**Usage:**

```
**bold text**
```

**Type:**

: `bold` :
:-- `Single`
:
: Element type for bold inline formatting.

### Italic

A text is italic by surrounding it with `*`.

**Usage:**

```
*italic text*
```

**Type:**

: `italic` :
:-- `Single`
:
: Element type for italic inline formatting.

### Underline

A text is underlined by surrounding it with `__`.

**Usage:**

```
__underlined text__
```

**Type:**

: `underline` :
:-- `Single`
:
: Element type for underline inline formatting.

### Overline

A text is overlined by surrounding it with `‾` (U+203E).

**Usage:**

```
‾overlined text‾
```

**Note:** This non-ASCII based character was chosen, since no ASCII based combination was intuitive enough.

**Type:**

: `overline` :
:-- `Single`
:
: Element type for overline inline formatting.

### Strike through

A text is strike through by surrounding it with `~~`.

**Usage:**

```
~~strike through text~~
```

**Type:**

: `strikethrough` :
:-- `Single`
:
: Element type for strike through inline formatting.

### Superscript

A text is superscripted by surrounding it with `^`.

**Note:** This formatting may not be stacked with subscript formatting.

**Usage:**

```
^superscripted text^
```

**Type:**

: `superscript` :
:-- `Single`
:
: Element type for superscript inline formatting.

### Subscript

A text is subscripted by surrounding it with `_`.

**Note:** This formatting may not be stacked with superscript formatting.

**Usage:**

```
_subscripted text_
```

**Type:**

: `subscript` :
:-- `Single`
:
: Element type for subscript inline formatting.

### Verbatim

A text may be defined as verbatim by surrounding it with `` ` ``.
If you want to use a `` ` `` inside, you can either escape `` ` `` using `\`,
or using the macro `{@um.plain()}`.

**Note:** Use `\\` to render a single backslash.

**Note:** This formatting must be the most inner formatting for stacked formatting, since every content inside is considered as plain text.

**Usage:**

```
`verbatim text`

`{@plain(`)}` or `\``

`char{@plain(`)}` or `char\``
```

**Type:**

: `inline-verbatim` :
:-- `Single`
:
: Element type for verbatim inline formatting.

**Attribute:**

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

### Highlight

A text may be highlighted by surrounding it with `||`.

**Usage:**

```
||highlighted text||
```

**Type:**

: `highlight` :
:-- `Single`
:
: Element type for highlight inline formatting.

### Quote

A text may be quoted by surrounding it with `""`.

**Usage:**

```
""quoted text""
```

**Type:**

: `inline-quote` :
:-- `Single`
:
: Element type for quote inline formatting.

## Inline math mode

Inline math mode may be used by surrounding formulas with `$`.
More information about math mode may be found in the [math mode definition section](#math-mode).

**Usage:**

```
$\frac{1}{n}$
```

**Type:**

: `inline-math` :
:-- `Single`
:
: Element type for inline math mode elements.

**Attributes:**

- [Text attributes](#text-attributes)

## Inline text group

Text inside one paragraph may be grouped by surrounding it with `[]`. Only inline elements may be used inside a text group.
Attributes may be set after the closing `]` of the text group.

**Note:** Any `[` must be closed with `]`. Otherwise, rendering must fail.

**Note:** To use `[` without `]`, it must be escaped like `\[`.

**Usage:**

```
A paragraph with [grouped text]{ "size" : "20pt" }. Also grouping within one w[or]{ "color" : "rgb(255,0,0)" }d is possible.
```

**Type:**

: `textgroup` :
:-- `Single`
:
: Element type for inline text group elements.

**Attributes:**

- [Text attributes](#text-attributes)

## Hyperlink

A hyperlink is set with `[<displayed text>](<link>)`, where the displayed text may only have inline elements.
Hyperlinks may be set to external sources by setting a URL as link, or IDs. For IDs, the given link must start with a `#` followed by the ID.
It is possible to set a link title using the `"title"` attribute. If it is not set, the URL is shown. If no character is set inside `()`, the displayed text is taken as link.
Attributes may be set after the closing `)` of the URL.

Elements of other documents can be linked, by setting `<link to other document>#<element id>` as link.

**Note:** As with text groups, any `(` must be closed with `)`. Otherwise, rendering must fail.

**Note:** Hyperlinks with IDs as sources should only be used, if an explicit text is wanted. Otherwise, [ID referencing](#id-referencing) should be used.

**Usage:**

```
[Text represented as hyperlink](/some/url)

[Explicit hyperlink text for some element](#element-id)

[Hyperlink with an explicit title](some-url){ "title" : "Explicit hyperlink title" }

[https://github.com/]()

[Requirements.md#stick-to-unimarkup]()
```

**Type:**

: `hyperlink` :
:-- `Single`
:
: Element type for inline hyperlink elements.

**Attributes:**

- [Text attributes](#text-attributes)

: `title` :
:-- `text`
:
: Optional link title that is displayed instead of the URL.

## Inline image

Images may be inserted inside a paragraph using `[!!<alternate text>](<image url>)`.
The alternate text is shown if the image may not be found, or may be used by screen readers.
It is only possible to use plain text as alternate text.
Optional attributes are set after the closing `)` of the URL.

**Note:** Same restrictions regarding closing as with hyperlinks apply.

**Usage:**

```
Some paragraph text with [!!some image](<image url>).

[!!<alternate text for this image>](<image url>){<inline image attributes>}
```

**Type:**

: `inline-image` :
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

## Inline file insert

There are two different ways to insert files inside a paragraph.
The general form of an inline file insert looks like a hyperlink with a **special character sequence** set immediately after `[`.
Optional attributes are set after the closing `)` of the URL.

**Note:** If the inserted content does not fit inside a paragraph, no content is inserted.

**Note:** The description given inside `[]` is only used as information about the content of the inserted file. The text will not be in the rendered document.

**Type:**

: `inline-insert` :
:-- `Group`
:
: Group type for inline file insert elements.

**Attribute:**

: `insert-id` :
:-- `text`
:
: An ID of a paragraph element of the inserted file may be set, to only include the content of this paragraph,
: even if the file itself would have more content, and could not be inserted as inline. 

### Rendered inline file insert

Using `''` as special character sequence renders the inserted file depending on the file type.
Supported file types depend on the available renderer. See [additional renderer](#additional-renderer) for more information.

**Usage:**

```
[''<description for the file content that is inserted>](<file path>){<attributes>}

[''First heading note](Unimarkup_Language_ReferenceManual.md){ "insert-id" : "first-heading-note" }
```

**Type:**

: `rendered-inline-insert` :
:-- `Single`
:
: Element type for inline rendered file insert elements.

**Attribute:**

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

### Verbatim inline file insert

Using ` `` ` as special character sequence inserts the text of a file as is like inline verbatim formatting. Every plain text format may be inserted.
An optional text highlighter may be set as attribute. See [additional highlighter](#additional-highlighter) for more information on available highlighter.

**Note:** To have `[` at the end of an inline verbatim, you must not set another open verbatim immediately afterwards.

**Usage:**

```
[``<description for the file content that is inserted>](<file path>){<attributes>}

Some paragraph text with [``First heading note](Unimarkup_Language_ReferenceManual.md){ "insert-id" : "first-heading-note" }.

`[`open bracket is part of inline verbatim]()

`[``verbatim insert]() -> open verbatim is never closed
```

**Type:**

: `verbatim-inline-insert` :
:-- `Single`
:
: Element type for inline verbatim file insert elements.

**Attribute:**

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

## Explicit substitution

Explicit substitution may be used to replace a word by inline content.
For this, the word to be substituted must be enclosed by `::`.

[Emoji aliases](https://github.com/github/gemoji/blob/master/db/emoji.json)
are already predefined for substitution, substituting the alias with the respective Unicode glyph.

Additional words may be defined for substitution using the `um.addSubstitution` macro.

## Direct substitution
### Emoji substitution

Some special character sequences are reserved for direct emoji conversion. Those sequences must be surrounded by white-spaces, or they are kept as is.

**Full list of available direct emojis:**

- `:)` ... 🙂 (U+1F642) has aliases: `slightly_smiling_face`
- `;)` ... 😉 (U+1F609) has aliases: `wink` 
- `:D` ... 😃 (U+1F603) has aliases: `smiley`
- `^^` ... 😄 (U+1F604) has aliases: `smile` **Note:** Must not be treated as superscript open/close.
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
- `--` ... 😑 (U+1F611) has aliases: `expressionless`
- `<3` ... ❤ (U+2764) has aliases: `heart`
- `(Y)` ... 👍 (U+1F44D) has aliases: `+1`, `thumbsup`
- `(N)` ... 👎 (U+1F44E) has aliases: `-1`, `thumbsdown`

**Usage:**

```
A text with an emoji :D in it!
```

Rendered to:

```
A text with an emoji 😃 in it!
```

**Type:**

: `emoji` :
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

```
A text --> using an arrow!
```

Rendered to:

```
A text 🠖 using an arrow!
```

**Type:**

: `arrow` :
:-- `Single`
:
: Type for arrow translation.

## Referencing

There are several reference variations in Unimarkup.

**Type:**

: `reference` :
:-- `Group`
:
: Group type for reference elements.

### Notes

Notes may be used to reference additional content that should not be part of the normal document flow.
The `{%um.notes}` list contains all notes that have been referenced up until the current position in the document, where the list is accessed.

A note may be referenced inside a paragraph with `[^^<note-id>]`.

**Note:** The macro [`{@<definition> um.addNote{%id%content}}`](#predefined-macros) must be used to define the note content. 

**Usage:**

```
Referencing a note [^^note-id] and [^^myNote].
```

**Type:**

: `note-reference` :
:-- `Single`
:
: Element type for referencing defined notes.

### ID referencing

Every heading and block element of an Unimarkup file may be referenced by its ID using `[##<element-id>]`.
To reference an element that is part of the Unimarkup document, but not in the same Unimarkup file,
the namespace of the Unimarkup file of the element must be set like `[##<namespace>##<element-id>]`.

**Note:** If the element-id contains `##`, it must be escaped to not be considered as namespace.

To define the text that is shown when an element is referenced, the attribute `ref-option` may be used.
Attributes are set after the closing `]`.

**Usage:**

```
[!!Some image](<image url>){ "id" : "some-image-id", "ref" : { "label" : "Some image" } }

A paragraph that references [##some-image-id]{ "refOption" : "label" }. 
The referenced text looks like: Some image
```

**Type:**

: `id-reference` :
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

### Literature referencing

Literature references are used to reference books, articles, journals or websites and use the [Citation Style Language](https://citationstyles.org/) to render literature depending on the provided CSL file.
To reference a literature, the literature meta-data and CSL file must be provided using one of the [configuration options](Configuration_Reference.md).
The literature meta-data must be in a format that is supported by the used CSL processing tool. See the documentation of the used Unimarkup implementation for more information.

A literature is referenced using the ID (called *label* in BibTeX) of a literature entry in the form `[&&<literature-id>]`.
It is possible to reference more than one literature with `[&&<first-literature-id>&&<second-literature-id>]`.

Depending on the used CSL, citations are either `in-text` or `note`. More information may be found in the [CSL specification](https://docs.citationstyles.org/en/1.0.1/specification.html).
In the `note` variant, literature references are treated like [notes](#notes), but references are not added to the note list.
Referenced literatures, used up to the current position in the document, are stored in the list `{%um.usedLiterature}`.

**Note:** If a literature has more than one definition, the behavior depends on the used CSL processor tool.

**Note:** Literature ID restrictions depend on the used CSL processor tool, but must not include `&`, `.` and `]`.

**Usage:**

```
This text has some literature reference [&&literature-id]
This text has more than one literature reference [&&id-1&&id-2].
```

**Type:**

: `literature-reference` :
:-- `Single`
:
: Element type for literature references.

### Distinct Reference

A distinct reference may be used to explicitly state the property of a literature reference that is to be inserted.
For this, the literature ID must be surrounded by `&&`. The property may optionally be set following a `.` after the ID.
If no property is set, `authors` is chosen as fallback.

**Note:** The same ID constraints apply as defined for [literature referencing](#literature-referencing).

**Usage:**

```
&&Gruber2004&& invented &&Gruber2004.title&& in &&Gruber2004.year&&.

The above is converted into:

John Gruber invented Markdown in 2004.
```

**Note:** The ID Gruber2004 must be set accordingly in the given references for the above example.

**Type:**

: `distinct-reference` :
:-- `Single`
:
: Element type for distinct referencing.

## Abbreviation

Abbreviations may be used as substitution or tooltip with the syntax `[::<abbreviation>]`. The full text of an abbreviation may then be displayed as tooltip depending on the output format.

An abbreviation must not end with `::`, as it would be taken as an explicit substitution.

The list `{%um.abbreviations}` holds all used abbreviations in the document up to the current position.

**Note:** If an abbreviation is defined more than once, rendering must fail.

**Usage:**

```
Some text using an [::abbr]. 

Text using abbreviations [::xml], [::html] and [::OPC UA TSN].
```

**Type:**

: `abbreviation` :
:-- `Single`
:
: Element type for inline abbreviations.

## Direct Unicode

Any Unicode code point may be inserted in Unimarkup with `&<Unicode code point>;`. Where the *Unicode code point* is given in the form `U+<HEX value>`.

**Usage:**

```
&U+1F642;
```

**Type:**

: `direct-unicode` :
:-- `Single`
:
: Element type for inline Unicode.

## Comment

Unimarkup provides line comments using `;;` to start a comment.
Optionally, a comment can be ended using `;;`, to end a comment before the end of a line. 

**Note:** It is not possible to have a backslash at the end of a line to get an explicit new line, if a comment is not closed.

**Usage:**

```
;; comment to end of line

A comment may be ;; end of line comment
at the end of a line

Comment ;;this is a comment;; inside one line.
```

**Type:**

: `comment` :
:-- `Single`
:
: Element type for Unimarkup comments.

## Inline field

This element adds a field name at the start of an inline text group that is enclosed inside `<>`.
This field name may be used for certain output formats or extensions.
If a field name is not known by an output format, or no extension is available to handle the field name, the inline field
is treated as a normal [inline text group](#inline-text-group). Optional flags must be set before the field name. 

**Note:** `<>` is not a placeholder in the usage examples.

**Usage:**

```
[<field name> Some inline content]

[?someFlag?<someField> Some inline content]
```

**Type:**

: `inline-field` :
:-- `Single`
:
: Element type for an inline field.
