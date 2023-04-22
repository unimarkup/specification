# Verbatim block insert

The general syntax for the verbatim block insert is described in the general [inline insert](/markup/inlines/boxes/inserts/README.md) section.

The keyword for verbatim inserts is ` `` `.

This insert applies verbatim formatting to the resource content.
The content itself is treated as plain text, with optional syntax highlighting applied to the content.

**Usage:**

```
``[<alternative description for the file content that is inserted>](<file path>)

``[First and second heading](UnimarkupContent.um){ insert-ids : "first-heading" "sec-heading" }
```

**Type:** `verbatim-block-insert`

**Attributes:**

- `language` ... The name of the resource language (e.g. markdown, rust, ...)

  **Note:** The supported languages depend on the used highlighter.

  **Note:** If the language is not supported by the highlighter, the content must be treated as plain text.

- `highlighter` ... The highlighter used for syntax highlighting of the resource content

  **Note:** The supported highlighters depend on the used implementation.
  
  **Note:** If the highlighter is not supported by the implementation, the content must be treated as plain text.

**Note:** Implementations may allow additional attributes.
