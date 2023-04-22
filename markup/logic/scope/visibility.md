# Visibility

**WIP**

Visibility defines where a logic element is accessible.

## Top level defined

Logic elements defined at the highest level in a file are visible in the whole file.

**Example:**

```
{#const TopLevel := 1/}
```

## Inside enclosed or indented elements

Logic elements defined in an enclosed or indented element are only visible inside the element.

**Example:**

```
[[[
  {#const InsideTextblock := 2/}
]]]
```

## Inside macros

Like with enclosed elements, logic elements defined inside a macro body are also only visible inside the body.

## Rendered inserts

If a Unimarkup file is inserted via a [rendered insert](/markup/blocks/inserts/render-block-insert.md), the visibility of logic elements depends on the name of an element.

### Private logic elements

If the name of a logic element starts with `_`, the element is private.
Private logic elements are only accessible in the file they are defined.

### Public logic elements

All logic elements not starting with `_` are public.
The visibility of logic elements is as if the content was copied to the inserted position.
