# Render block

Render blocks use `'` as keyword.

Content inside a render block is rendered according to the given language and renderer.
Backslash escapes may be used inside render blocks as described in [/markup/escaping](/markup/escaping).

A language may be set after the start keyword, by setting the name of a language directly after `'`. An implementation may choose the best supported renderer for the given language.
Alternatively, attributes may be set instead of the language name.

**Note:** If attributes span multiple lines, the first line after attributes are closed start the render content.

**Note:** Render block nesting is not allowed.

**Usage:**

```
'''mermaid
graph TB
    A & B--> C & D
'''
```

**Type:** `render-block`

**Attributes:**

- `language` ... Sets the name of the language that should be rendered

  **Note:** Languages must not contain any whitespace.

  **Note:** Supported languages depend on the used renderer.

- `renderer` ... The renderer used to render the content into Unimarkup block elements

  **Note:** The supported renderer depend on the used implementation.
  
  **Note:** If the renderer is not supported by the implementation, the content must be treated as plain text.

**Note:** Implementations may allow additional attributes.
