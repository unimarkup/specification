# Definition list

The general list syntax is described in the [lists](/markup/blocks/indents/lists/README) section.
A definition list is a bullet list, where all entry headings start with one or more definition terms that are separated by `|`,
followed by the sequence `...` set after the terms. The `...` sequence must be surrounded by at least one whitespace.
The first definition description may be given directly after the `...` sequence, and all further description blocks must be correctly indented, and separated by blank lines.

**Usage:**

````
- Bullet list ... Gets transformed to a definition list
- Possible `option` ...

  Description for the `option` term.

- Multiple `paragraphs` ... As with bullet lists

  Multiple paragraphs are possible.

- Nested ... definition list
  + Works ... too

- Definition | term ... With multiple terms
````

**Type:** `definition-list`
