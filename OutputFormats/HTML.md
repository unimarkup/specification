# HTML output format

Defines how Unimarkup elements are converted to the HTML output format,
and lists additionally supported fields and configuration options.

**Table of content:**

- [Inline elements](#inline-elements)
- [Atomic block elements](#atomic-block-elements)
- [Enclosed block elements](#enclosed-block-elements)
- [Additional inline fields](#additional-inline-fields)
- [Additional field blocks](#additional-field-blocks)
- [Additional configuration options](#additional-configuration-options)
- [Handling special HTML characters](#handling-special-html-characters)

## Inline elements

- **Bold**

  `**bold text**` renders to `<strong>bold text</strong>`

- **Italic**

  `*italic text*` renders to `<em>italic text</em>`

- **Underline**

  `__underlined text__` renders to `<u>underlined text</u>`

- **Overline**

  `‾overlined text‾` renders to `<span style="text-decoration: overline;">overlined text</span>`

- **Strike through**

  `~~strike through text~~` renders to `<span style="text-decoration: line-through;">strike through text</span>`

- **Superscript**

  `^superscript text^` renders to `<sup>superscript text</sup>`

- **Subscript**

  `_subscript text_` renders to `<sub>subscript text</sub>`

- **Verbatim**

  `` `verbatim text` `` renders to `<pre>verbatim text</pre>`

- **Highlight**

  ;;mhatzl

- **Quote**

  ;;mhatzl

- **Inline math mode**

  ;;mhatzl

- **Inline text group**

  There are two variations:

  1. No attributes set

    If no attributes are set for an inline text group, the text is taken as is without surrounding it with any HTML tag.

    `outside text [*plain* text group]` renders to `<p>outside text *plain* text group</p>`

  2. Attributes set

    Text attributes are converted to style properties.

    `[text group]{<some attributes>}` renders to `<span style="<converted attributes>">text group</span>`

- **Hyperlink**

  ;;mhatzl


- **Inline image**

  ;;mhatzl

- **Rendered inline file insert**

  The inserted content is interpreted depending on the set renderer,
  and then interpreted and output as Unimarkup content.

  **Note:** Only content that may be converted to inline elements is allowed to be inserted.

  `[''Some file description](someFile.um)` renders to `<strong>content</strong> of <pre>someFile.um</pre> that is <em>rendered</em>`

  **Note:** The above example assumes the content ``**content** of `someFile.um` that is *rendered*`` inside the file `someFile.um`.

- **Verbatim inline file insert**

  The inserted content is output as if it was surrounded by verbatim formatting.

  **Note:** Only content that may be converted to inline elements is allowed to be inserted.

  `[``Some file description](someFile.md)` renders to `<pre>content of someFile.md</pre>`

- **Comments**

  The behavior depends on the configuration option `keep-comments`.

  - Option set

    Comments are converted to HTML comments.

  - Option **not** set

    Comments are not forwarded to the resulting output file.

- **Inline field**

  See [additional inline fields](#additional-inline-fields) on available inline fields for the HTML output format.

## Atomic block elements

- **Heading**

  `# Heading level 1` renders to `<h1>Heading level 1</h1>`  
  `## Heading level 2` renders to `<h2>Heading level 2</h2>` 
  `### Heading level 3` renders to `<h3>Heading level 3</h3>`  
  `#### Heading level 4` renders to `<h4>Heading level 4</h4>`  
  `##### Heading level 5` renders to `<h5>Heading level 5</h5>`  
  `###### Heading level 6` renders to `<h6>Heading level 6</h6>`

- **Paragraph**

  `paragraph content` renders to `<p>paragraph content</p>`

- **Bullet list**

  ;;mhatzl

- **Numbered list**

  ;;mhatzl

- **Task list**

  ;;mhatzl

- **Definition list**

  ;;mhatzl

- **Table**

  ;;mhatzl

- **Figure insert**

  ;;mhatzl

- **Media insert**

  ;;mhatzl

- **Rendered block file insert**

  The inserted content is interpreted depending on the set renderer,
  and then interpreted and output as Unimarkup content.

- **Verbatim block file insert**

  The inserted content is output as if it was inside a verbatim block.

- **Quotation block**

  ;;mhatzl

- **Line block**

  ;;mhatzl

- **Definition block**

  ;;mhatzl

- **Horizontal line**

  `---` renders to `<hr/>`

- **Page break**

  A page break has three different output variants for the HTML output format.

  1. Used as column break inside an explicit column

    ;;mhatzl

  2. Used as regular page break with attributes

    All content up to the next page break is put inside a `div` block with the attributes set to the opening `div` tag.

    If a text group is opened, but not closed between page breaks, four `div` blocks are created in the following way:

    1. The first `div` block contains all elements until the text block start,
    and has the attributes of the first page break applied

    2. The second `div` block contains all elements between the text group start and the second page break, and has the attributes of the text group and first page break merged and applied with the text group attributes taking precedence

    3. The third `div` block contains all elements between the second page break and the text group end, and has the attributes of the text group and second page break merged and applied with the text group attributes taking precedence

    4. The fourth `div` block contains all further elements until a next page break, end of file, or a split page break text group constellation is reached again. The attributes of the second page break are applied.

  3. Used as regular page break without attributes

    `:::` renders to `<br/>`

## Enclosed block elements

- **Verbatim block**

  ;;mhatzl

- **Render block**

  ;;mhatzl

- **Math block**

  ;;mhatzl

- **Text block**

  ;;mhatzl

- **Explicit column block**

  ;;mhatzl

- **Implicit column block**

  ;;mhatzl

- **Form block**

  ;;mhatzl

## Additional inline fields

- `kbd` ... Defines keyboard input

  `[<kbd>input]` renders to `<kbd>input</kbd>`

- `samp` ... Defines sample program output

  `[<samp>output]` renders to `<samp>output</samp>`

## Additional field blocks

- `article` ... Defines an article region

  ```
  [[[<article>
    # Article heading

    Some content.
  ]]]
  ```

  renders to

  ```
  <article>
  <h1>Article heading</h1>
  <p>Some content.</p>
  </article>
  ```

- `aside` ... Defines a content to display aside other content

  ```
  [[[<aside>
    # Aside heading

    Some content.
  ]]]
  ```

  renders to

  ```
  <aside>
  <h1>Aside heading</h1>
  <p>Some content.</p>
  </aside>
  ```

## Additional configuration options

The following configuration options are only available for HTML output.

### Taking values

- `html-template` ...--`filepath`-- Set a template HTML file with `{{ head }}` set inside the `head` element and `{{ body }}` set inside the body element.

    Styling, fonts and scripts will be inserted at `{{ head }}`, and rendered Unimarkup content is placed inside `{{ body }}`.
    Optionally, `{{ toc }}` can be set to get the table of content 
    (**Note:** This will not remove a rendered table of content in the rendered Unimarkup content if present).

## Handling special HTML characters

The following characters would break plain text content in HTML, and must therefore be escaped automatically during rendering:

- `<` escaped as `&lt;`
- `<` escaped as `&gt;` (**Note:** Would not break HTML, but required for better consistency)
- `&` escaped as `&amp;`
