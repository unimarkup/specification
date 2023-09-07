# Render block

Render blocks use `'` as keyword.
Render block nesting is not allowed.

Content inside a render block is rendered according to the given language and renderer.
Backslash escapes may be used inside render blocks as described in [/markup/escaping](/markup/escaping.md).

A language may be set after the start keyword, by setting the name of the language directly after `'`.

**Usage:**

```
'''mermaid
graph TB
    A & B--> C & D
'''
```

**Type:** `render-block`

**Attributes:**

- `renderer` ... The renderer used to render the content into Unimarkup block elements

  **Note:** The supported renderer depend on the used implementation.
  
  **Note:** If the renderer is not supported by the implementation, the content must be treated as plain text.

  **Note:** Implementations may not offer this attribute if they only support one renderer.

- `sandbox` ... Set to `true` to exclude elements like headings from being added to the document section.

  **Note:** Implementations are free to define further rules that apply for this attribute.

**Note:** Implementations may allow additional attributes.
