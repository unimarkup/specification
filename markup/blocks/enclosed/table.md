# Table

**WIP**

Tables have `=` as keyword. Every line inside the table content is interpreted as one table row, except lines starting with `---` (see **table entry merging** below).
Column breakpoints are set using `|`. Rows and columns are internally numbered, starting with `row = 1, column = 1` at the top left. Both numbers are incremented by one per new row/column.

**Note:** It is not possible to nest tables. Use [column blocks](/markup/blocks/enclosed/columns/README.md) instead.

- **Table entry**

  A table entry is identified by the row and column number.
  The entry at row=1 column=1 is the top left entry.

  A table entry only allows inline elements.

- **Shorthand column styles**

  Common column styles may be set inside parentheses directly after the start sequence using special keywords. Columns are separated using `,`.
  The styles are applied left to right, and if not enough styles are set, the last set style must be used for the remaining columns.
  If more styles are set, they must be ignored, and an implementation should output a warning.

  - **Column kind**

    There are three column kinds:

    - `#` ... header column
    - `-` ... default (plain) column
    - `_` ... footer column

    **Usage:**

    ```
    ===(#, -, _)
    | header column | normal column | footer column |
    | header column | normal column | footer column |
    ===
    ```

  - **Alignment options**

    There are four alignment options:

    - `<column kind>` ... default alignment
    - `:<column kind>` ... left alignment
    - `<column kind>:` ... right alignment
    - `:<column kind>:` ... center alignment

    **Usage:**

    ```
    ===(-:, :-, -, :-:)
    | right aligned | left aligned | default alignment | center aligned |
    ===
    ```

- **Shorthand row kind**

  The row kind may be set at the start of the line.
  There are three row kind options:

  - `#|` ... heading row
  - `|` ... default row
  - `_|` ... footer row

  **Note:** Header rows are only allowed before the first normal or footer row.

  **Note:** Footer rows are only allowed at the end of a table.

  **Usage:**

  ```
  ===
  #| header row |
  #| 2nd header row |
  | normal row |
  _| footer row |
  ===
  ```

- **Table entry merging**
  
  Rows may be combined with the previous one, by using `+|` at the beginning of the line.
  To only combine specific columns, a new line must start with `---`, followed by a shorthand column style with `+` marking the column to merge.

  **Note:** It is not allowed to combine full row merge and specific column merge.

  **Usage:**

  ```
  ===
  | merged | merged |
  +| rows  | rows   |
  ===

  ===
  | column 1 | column 2 | column 3 |
  ---(-,+,-)
  | column 1 | merged column 2 | column 3 |
  ===
  ```

**Usage:**

```
===(-:, :-, :-, :-:)
| right aligned | left aligned | spanning | center aligned |
---(-, -, +, -)
| settings kept | settings kept | two rows | settings kept |
---
| settings kept | settings kept | new row | settings kept |
===

===
#| header row |
#| 2nd header row |
| normal row |
_| footer row |
===

===
#| header row |
+| merged header row |
| normal row |
_| footer row |
+| merged footer row |
===

===(#, -, _)
| header column | normal column | footer column |
| header column | normal column | footer column |
===

===
| merged | merged |
+| rows  | rows   |
===

===
| small column | combined +| columns |
| combined +| columns | small column |
===

===
small column | combined +| columns
combined +| columns | small column
===

===(:-, :-:)
| row 1 | row 1 | row 1 |
| row 2 | row 2 | row 2 |
==={<attributes for all columns>}

===(:-:)
| center row 1 | center row 1 | center row 1 |
| center row 2 | center row 2 | center row 2 |
==={ id: "table-id" }

===
| row 1 | row 1 | row 1 |
| row 2 | row 2 | row 2 |
==={<attributes for all columns>}

===
| row 1 | row 1 | row 1 |
| row 2 | row 2 | row 2 |
==={<attributes 
  for all columns
  over multiple lines
>}
```

**Type:** `table`
