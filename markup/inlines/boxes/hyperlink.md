# Hyperlink

A hyperlink is set with `[<displayed text>](<link> <optional title>)`, where the displayed text may only have inline content.
Hyperlinks may be set to external sources by setting a URL as link.
Links to sources in the same domain may be located by setting the path to the source as link.
To link to elements of a document, the ID of the element to link to must be set after one `#`.
It is possible to set an optional link title after the link. At least one whitespace must be between link and title.
If no title is set, the link is used as title.
If no displayed text is set, the link is used as display text.

**Note:** Link and title must be treated as plain text without any markup being applied.

**Note:** Any `(` must be closed with `)`. Otherwise, rendering must fail.

**Note:** Use [ID referencing](/markup/inlines/boxes/referencing/id-reference) instead of hyperlinks to link to elements if you do not need an explicit title.

**Usage:**

```
[Text represented as hyperlink](/some/path)

[Explicit link title for some element](#element-id takes you to the element)

[Hyperlink with an explicit title](some-url Explicit hyperlink title)

[](https://github.com/)
```

**Type:** `hyperlink`
