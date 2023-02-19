# Abbreviation

**WIP**

Abbreviations may be used with `[::<abbreviation>]`, where the abbreviation is treated as plain text and must not contain `:` and `]`.

To set the full text for an abbreviation, write the full text after the abbreviation separated by `:`.

**Note:** The first full text found in document flow for an abbreviation must be used for all further abbreviations.

**Note:** If a full text is given more than once for the same abbreviation, the later full text is ignored, and a warning must be output.

**Note:** If no full text is set for an abbreviation, a warning must be output. 

**Note:** For better accessibility, the full text must be shown in parentheses `()` after the first use of the abbreviation in document flow. Abbreviation and `(` should be separated by one space.

**Note:** In HTML, no *title* attribute should be set, since this would cause screen readers to read the full text every time the abbreviation is used. Therefore, only the first abbreviation use has the full text displayed in parentheses. 

**Usage:**

```
Some text using an [::abbr: abbreviation].

Text using abbreviations [::xml], [::html] and [::OPC UA TSN].
```

The first line in the usage example would render to

```
Some text using an abbr (abbreviation).
```

**Type:** `abbreviation`
