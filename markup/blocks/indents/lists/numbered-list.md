# Numbered list

The general list syntax is described in the [lists](/markup/blocks/indents/lists/README) section.
A numbered list entry has a positive integer number followed by `.` as keyword.
The number of the first entry defines the start number of the list.
Numbered lists are automatically incremented by 1 per new list entry,
so it is not needed to manually increment the number.

**Note:** The number may be manually incremented per list entry, but a warning should be output if the order is wrong.

**Usage:**

````
1. Start of numbered list
  1. Sub numbered list

1. Second entry in main numbered list

  Paragraph for this numbered list

  Other paragraph for this numbered list

  ```
  Verbatim block for this numbered list
  ```

  1. Sub numbered list

    Paragraph for this sub numbered list

/

3. Numbered list starting at specific number
3. Numbered list element that gets incremented automatically
````

**Type:** `numbered-list`
