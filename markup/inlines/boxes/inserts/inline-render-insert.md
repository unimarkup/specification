# Inline render insert

The general syntax for the inline render insert is described in the general [inline insert](/markup/inlines/boxes/inserts/README) section.

The keyword for render insert is `''`.

This insert tries to convert the resource content into Unimarkup inline elements.

**Usage:**

```
[''<alternative text for the file content that is inserted>](<file path>)

[''First heading](SomeUnimarkupContent.um){ "insert-id" : "first-heading" }
```

**Type:** `inline-render-insert`

**Attributes:**

- `language` ... The name of the resource language (e.g. markdown, rust, ...)

  **Note:** The supported languages depend on the used renderer.

  **Note:** If the language is not supported by the renderer, the content must be treated as plain text.

- `renderer` ... The renderer used to convert the resource into Unimarkup inline elements

  **Note:** The supported renderer depend on the used implementation.
  
  **Note:** If the renderer is not supported by the implementation, the content must be treated as plain text.
