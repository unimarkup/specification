# Special substitution

Certain keywords may be substituted for Unicode code points representing special graphemes.
Those keywords may appear anywhere in an inline content.

**Note:** Some keywords may behave differently depending on the context.

**List of supported special grapheme substitutions:**

- `((TM))` or `((tm))` ... ™ (U+2122)
- `((C))` or `((c))` ... © (U+00A9)
- `((R))` or `((r))` ... ® (U+00AE)
- `...` ... … (U+2026)

  **Note:** `...` is not converted to a horizontal ellipsis if it is used to form a [description list](/markup/blocks/indents/lists/description-list.md). 

- `(+-)` or `(-+)` ... ± (U+00B1)
- `--` ... – (U+2013)

  **Note:** The en dash must not be surrounded by other `-`.

- `---` ... — (U+2014)

  **Note:** The em dash must not be surrounded by other `-`.

  **Note:** `---` is treated as [horizontal line](/markup/blocks/separators/horizontal-line.md) if it is surrounded by blank lines.

**Usage:**

```
Trademark((tm)) and (+-) ""2023--"".
```

renders to

```
Trademark™ and ± “2023–”.
```

**Type:** `special-substitution`
