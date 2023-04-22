# Lists

This section contains all available list elements in Unimarkup.
List elements are a subset of indented blocks in Unimarkup.
The general syntax for indented blocks is described in the general [indented block](/markup/blocks/indents/README.md) section.

**Type:** All list elements are subtypes of the `um-list` type.

## List scope

A list is started by the first line that starts with the list keyword.
Every element that starts with the list keyword is referred to as `list entry`.
A list entry may contain indented elements including other lists.
The block content set directly after the keyword is referred to as `list entry heading`.

The list implicitly ends before the first element in document flow that is not indented to the required depth.

## Nesting different list types

  Nested lists of different types may not have a blank line between the list entry of the parent, and the first list entry of the nested list.
  
  **Note:** If the list type changes at the same depth, it must be treated as a new list.

  **Examples:**

  ```
  - Bullet list
    1. Sub numbered list

  1. New numbered list
    - Sub bullet list
  ```

## Explicitly dividing lists

Since lists are ended implicitly, every list entry of the same list type will be combined in one list, as long as the indentation is fulfilled.

To explicitly split list entries in separate lists, a backslash may be set at the start of a line between the list entries that should be split.
This breaks indentation, and results in two separate lists.

**Example:**

```
- list 1

\

- list 2
```

## List attributes

It is not possible to set list attributes, but list entry attributes may be applied per list entry at the end of the list entry heading.

**Note:** The list entry heading attributes only apply to the entry heading, and not to the remaining content of the list entry.

**Example:**

```
- bullet list entry heading {<with attributes>}
```
