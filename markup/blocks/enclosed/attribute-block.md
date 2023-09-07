# Attribute block

**WIP**

General styles for Unimarkup elements may be set, using the element type as class selector.
Nesting attributes is done as defined in the [CSS nesting module](https://www.w3.org/TR/css-nesting-1/), and as a consequence, nesting attribute blocks is not allowed.

**Note:** Attributes defined in an attribute block affect the whole document **independent** of their position in the document flow.

**Note:** Attributes `id` and `class` are not allowed for attribute blocks.

**Usage:**

```
{{{
  .bullet-list {
    <general bullet list attributes>
  }
  .numbered-list {
    <general numbered list attributes>
  }
}}}
```
