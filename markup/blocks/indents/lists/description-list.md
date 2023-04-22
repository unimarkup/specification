# Description list

The general list syntax is described in the [lists](/markup/blocks/indents/lists/README.md) section.
A description list is a bullet list, where all entry headings start with one or more description terms that are separated by `|`,
followed by the sequence `...` set after the terms. The `...` sequence must be surrounded by at least one whitespace.
The first description may be given directly after the `...` sequence, and all further Unimarkup blocks must be correctly indented, and separated by blank lines.

**Usage:**

````
- Bullet list ... Gets transformed to a description list
- Possible `option` ...

  Description for the `option` term.

- Multiple `paragraphs` ... As with bullet lists

  Multiple paragraphs are possible.

- Nested ... description list
  + Works ... too

- Description | term ... With multiple terms
````

**Type:** `description-list`
