# Inline formatting

Inline formatting consists of keywords that format an enclosed text in a certain way.

**Type:** All inline formattings are subtypes of the `formatting` type.

## Restrictions

A none-whitespace grapheme must immediately follow an opening keyword for inline formatting.
If the inline formatting is not closed by the same keyword with a none-whitespace grapheme before the closing keyword, no formatting is applied.

**Note:** Verbatim formatting is an exception and is applied independent of whitespaces.

**Note:** Inline formatting may also be applied inside words.

**Example:**

```
For*matt*ing inside __word__s is possible.
```

**Examples with no/partial formatting:** 

The following examples show text with formatting keywords, but no/partial formatting is applied, because not all requirements are fulfilled.

```
Text with* italic keyword followed by a whitespace.

Text *with correct italic opening keyword, but paragraph ends without closing keyword.

Text *with correct opening keyword, *but closing keyword is preceded by a whitespace.

Text ***with correct bold and italic opening keyword, but* only italic closing keyword is correct with bold not being applied.

Text ***with correct bold and italic opening keyword, but** only bold closing keyword is correct with italic not being applied.
```

## Format stacking

With format stacking, multiple inline formats are applied to the same inner text.
This is achieved by nesting formatting keywords.

**Note:** Not all formatting may be combined and some require certain order. Those restrictions are noted at the corresponding formatting definitions.

**Example:**

```
Stacking this **__text to be bold and underlined__**.

The opposite way __**is also bold and underlined**__.

To get ***bold and italic***.

Having a **`bold verbatim text`**.

Combining ^‾overlined superscript‾^ text.
```

**Special cases:**

- Fallback handling

  Formatting is started at the beginning of an inline content. If a formatting keyword is reached, it is parsed until another formatting keyword is encountered.
  The inner keyword is first tried to be completed, but if an end keyword of the outer format is encountered before the inner formatting is completed, the inner format is ignored, the inner start keyword is treated as plain text, and the outer format is applied.
  If a formatting is not closed at the end of an inline content, it is not applied, and the start keyword is treated as plain text.

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

- Order of formattings sharing the same keyword

  `bold` and `italic` share `*` and `subscript` and `underline` share `_`.
  This section handles the different combinations for those inline formats.

  If `bold` and `italic` are directly stacked, the order depends on the closing keyword.
  Otherwise, `**` is always taken as `bold`, and not as opening and/or closing `italic`.

  **Note:** The same applies for `subscript` and `underline`.

  1. Start and end are stacked

    The order does not matter, since all `*` are part of keywords, and the containing text gets both formats.

    ```
    ***bold and italic***
    ```

  2. Start is stacked, but `bold` ends before `italic`

    The outer `*` is considered part of `italic`, and the inner `**` part of `bold`.

    ```
    ***bold and italic** only italic*
    ```

  3. Start is stacked, but `italic` ends before `bold`

    The outer `**` is considered part of `bold`, and the inner `*` part of `italic`.

    ```
    ***bold and italic* only bold**
    ```

  4. End is stacked, but `bold` starts before `italic`

    The outer `**` is considered part of `bold`, and the inner `*` part of `italic`.

    ```
    **only bold *bold and italic***
    ```

  5. End is stacked, but `italic` starts before `bold`

    The outer `*` is considered part of `italic`, and the inner `**` part of `bold`.

    ```
    *only italic **bold and italic***
    ```

- Exceeding defined keyword sequence length of inline formats 

  If a keyword sequence exceeds the length usable for inline formats, the keyword sequence is treated as plain text.
  For example, having four or more contiguous `*` or `_` exceeds the maximum sequence length that leads to a valid inline formatting.
  In case of keywords like `|` and `~`, the maximum sequence length would be two, and so on.

  **Note:** Contiguous means the same keywords without any whitespace between.

  **Note:** This rule prevents empty formatting elements, because `****` is treated as plain text.

  ```
  ****plain**bold**
  ```

  The above renders to

  ```
  ****plain<bold start>bold<bold end>
  ```

## Attribute positioning

Attributes may be set directly after a closing keyword.
The allowed attributes may depend on the output format, and only special attributes are defined explicitly.

**Example:**

```
**bold with attributes**{ font-weight: 900 }
```

# Formatting options in Unimarkup
## Bold

A text is bold by surrounding it with `**`.

**Usage:**

```
**bold text**
```

**Type:** `bold-formatting`

## Italic

A text is italic by surrounding it with `*`.

**Usage:**

```
*italic text*
```

**Type:** `italic-formatting`

## Underline

A text is underlined by surrounding it with `__`.

**Usage:**

```
__underlined text__
```

**Type:** `underline-formatting`

## Overline

A text is overlined by surrounding it with `‾` (U+203E).

**Note:** This non-ASCII based character was chosen, since no ASCII based combination was intuitive enough.

**Usage:**

```
‾overlined text‾
```

**Type:** `overline-formatting`

## Strike through

A text is strike through by surrounding it with `~~`.

**Usage:**

```
~~strike through text~~
```

**Type:** `strikethrough-formatting`

## Superscript

A text is superscripted by surrounding it with `^`.

**Note:** This formatting may not be stacked with subscript formatting.

**Usage:**

```
^superscripted text^
```

**Type:** `superscript-formatting`

## Subscript

A text is subscripted by surrounding it with `_`.

**Note:** This formatting may not be stacked with superscript formatting.

**Usage:**

```
_subscripted text_
```

**Type:** `subscript-formatting`

## Verbatim

A text may be defined as verbatim by surrounding it with `` ` ``.
If you want to use a `` ` `` inside, you may escape `` ` `` using `\`.

**Note:** Use `\\` to render a single backslash.

**Note:** This formatting must be the most inner formatting for stacked formatting, since every format inside is considered as plain text.

**Usage:**

```
`verbatim text`

`\`` or `some text\` with escaped keyword`
```

**Type:** `verbatim-formatting`

**Attributes:**

- `language` ... Sets the name of the markup/programming language that is displayed in the verbatim body

  **Note:** Languages must not contain any whitespace.

  **Note:** Supported languages depend on the used highlighter.

- `highlighter` ... The name of the highlighter that should be used

  **Note:** The name must not contain any whitespace.

  **Note:** Supported highlighters may vary between Unimarkup implementations.

**Note:** Implementations may allow additional attributes.

## Highlight

A text may be highlighted by surrounding it with `||`.

**Usage:**

```
||highlighted text||
```

**Type:** `highlight-formatting`

## Quote

A text may be quoted by surrounding it with `""`.

**Note:** This is used to apply the correct quotes depending on the chosen locale.

**Usage:**

```
""quoted text""
```

**Type:** `quote-formatting`

## Math

Markup of mathematical expressions may be surrounded by `$$`.
These expressions are then placed alongside other inline content.

**Note:** The supported markup syntax for mathematical expression may vary between Unimarkup implementations.

**Example using [AsciiMath](http://asciimath.org/):**

```
$$sum_(i=1)^n i^3=((n(n+1))/2)^2$$
```

**Type:** `math-formatting`

**Attribute:**

- `markup-syntax` ... Sets the name of the markup syntax that is used inside math formatting.

  **Note:** If the given name is not supported by the implementation, the text including the keywords must be treated as plain text.

**Note:** Implementations may allow additional attributes.
