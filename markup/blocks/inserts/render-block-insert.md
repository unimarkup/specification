# Render block insert

The general syntax for the render block insert is described in the general [block insert](/markup/blocks/inserts/README) section.

The keyword for render inserts is `''`.

This insert tries to convert the resource content into Unimarkup block elements.
Parameters may be set after the URL, to use them for the content conversion.
Multiple parameters must be separated by `,`.

**Note:** Parameters for inserts of Unimarkup files map to the ones defined in the configuration of the inserted file.

**Usage:**

```
''[<alternative text for the file content that is inserted>](<url>)

''[First and second heading](SomeUnimarkupContent.um){ insert-ids : first-heading sec-heading }

''[Insert with parameters](unimarkup-file.um param1 := 2, param2 := 10)
```

**Type:** `render-block-insert`

**Attributes:**

- `language` ... The name of the resource language (e.g. markdown, rust, ...)

  **Note:** The supported languages depend on the used renderer.

  **Note:** If the language is not supported by the renderer, the content must be treated as plain text.

- `renderer` ... The renderer used to convert the resource into Unimarkup block elements

  **Note:** The supported renderer depend on the used implementation.
  
  **Note:** If the renderer is not supported by the implementation, the content must be treated as plain text.

- `sandbox` ... Set to `true` to exclude elements like headings from being added to the document section.

**Note:** Implementations may allow additional attributes.
