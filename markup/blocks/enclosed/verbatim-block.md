# Verbatim block

Verbatim blocks use `` ` `` as keyword.

Content inside a verbatim block is treated as is. No rendering is done, and all whitespace must be preserved.
The only exceptions are backslash escapes as described in [/markup/escaping](/markup/escaping).

A language may be set at the start of a verbatim block, by setting the name of a language directly after `` ` ``. An implementation may choose the best supported highlighter for the given language.
Alternatively, attributes may be set instead of the language name.

**Note:** If attributes span multiple lines, the first line after attributes are closed start the verbatim content.

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

**Type:** `verbatim-block`

**Attributes:**

- `language` ... Sets the name of the markup/programming language that is displayed in the verbatim body

  **Note:** Languages must not contain any whitespace.

  **Note:** Supported languages depend on the used highlighter.

- `highlighter` ... The name of the highlighter that should be used

  **Note:** The name must not contain any whitespace.

  **Note:** Supported highlighters may vary between Unimarkup implementations.

**Note:** Implementations may allow additional attributes.
