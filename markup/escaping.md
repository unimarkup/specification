# Escaping

All graphemes may be escaped using a backslash before them.
Escaping a grapheme always means that the escaped grapheme is taken literally.
For example, there is no special meaning for `\n` or `\t`.

**Note:** Escaping must work in all elements.

**Note:** Backslash escaping may also be used for inline verbatim to render `` ` ``.

**Note:** It is also possible to escape spaces and tabs, which must then be kept as is during rendering.

**Examples:**

```
\\ gets rendered to \
\$ gets rendered to $
\n gets rendered to n

\  escapes one space

`\`` gets rendered to <verbatim start>`<verbatim end>
```
