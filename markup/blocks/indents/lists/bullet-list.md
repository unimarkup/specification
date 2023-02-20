# Bullet list

Bullet lists start with either `-`, `*`, or `+` as keyword.
The general list syntax is described in the [lists](/markup/blocks/indents/lists/README) section.

**Note:** The different keywords may be used to define different list symbols.

**Usage:**

````
- Bullet list
  - Sub bullet list

- Second main bullet list entry

  Paragraph for this bullet list

  Other paragraph for this bullet list

  ```
  Verbatim block for this bullet list
  ```

  - Sub bullet list{ <bullet list entry attributes> }

    Paragraph for this sub bullet list

+ Bullet list entry with different symbol
  * Sub bullet list with different symbol

Paragraph not for a bullet list

- Bullet list with text
  that spans multiple lines
  but new lines are treated as spaces

/

- Backslash above defines this as a new bullet list
````

**Type:** `bullet-list`
