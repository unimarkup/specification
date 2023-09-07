# Verbatim block

Verbatim blocks use `` ` `` as keyword.
To nest verbatim blocks, the inner block must have at least one more `` ` `` than the outer one.

Content inside a verbatim block is treated as is. No rendering is done, and all whitespace must be preserved.
The only exceptions are backslash escapes as described in [/markup/escaping](/markup/escaping.md).

A language may be set at the start of a verbatim block, by setting the name of a language directly after `` ` ``.

**Usage:**

`````
```
Verbatim block, where nothing is rendered
```

```
Outer verbatim block.

````
Inner verbatim block.
````
```

```
Verbatim block with given attributes
```{<Attributes for the verbatim block>}

```C
int add(int a, int b) {
  return a + b;
}
```
`````

**Type:** `verbatim-block`

**Attributes:**

- `highlighter` ... The name of the highlighter that should be used

  **Note:** The name must not contain any whitespace.

  **Note:** Supported highlighters may vary between Unimarkup implementations.

  **Note:** Implementations may not offer this attribute if they only support one highlighter.

**Note:** Implementations may allow additional attributes.
