# Escaping

All graphemes may be escaped using a backslash before them.
Escaping a grapheme always means that the escaped grapheme is taken literally.
For example, there is no special meaning for `\n` or `\t`.

**Note:** Escaping must work in all Unimarkup elements, except inside attributes and preamble.

**Note:** Spaces and tabs may also be escaped, which must then keep them as is during rendering.

**Examples:**

```
\\ gets rendered to \
\$ gets rendered to $
\n gets rendered to n

\  escapes one space
```

## Explicit new line

A backslash `\` at the end of a line creates an explicit new line.

**Note:** Some elements may not allow a backslash at the end of a line.

**Note:** An explicit new line may have no effect in elements that keep all whitespace as is.

## Escaping verbatim content

Backslash escaping may also be used in verbatim content.
This allows to display the verbatim keyword inside verbatim formatting.

**Example:**

```
`\`` gets rendered to <verbatim start>`<verbatim end>

`some text\`` gets rendered to <verbatim start>some text`<verbatim end>
```
