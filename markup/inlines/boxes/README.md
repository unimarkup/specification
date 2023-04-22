# Inline boxes

Inline boxes are inline elements that use `[]` to surround inline content.
Some of those elements also allow additional information to be set using `()` directly after `]`.

**Type:** All box elements are subtypes of the `inline-box` type.

## Box elements

- `hyperlink`
- ...

## Restrictions

Any `[` must be closed with `]`. Otherwise, the remaining inline content is taken as plain.

**Note:** To use `[` without `]`, it must be escaped like `\[`.

**Example:**

```
**bold**, but [text group *content* taken as plain, because it is not closed.
```

## Box attribute positioning

Attributes may be set directly after `]` if no `()` is given for an element.
Otherwise, attributes may be set directly after the last `)`.
The allowed attributes may depend on the output format, and only special attributes are defined explicitly.

**Examples:**

```
[some green text]{ color: green }

[!!Some image](/path/to/an/image.png){ width: 50vw }
```
