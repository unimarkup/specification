# Attribute block

**WIP**

General styles for Unimarkup elements may be set, using the element type as class selector.

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



```
{{{
  p {
    color: green;
  }
}}}

[[[
{{{
  p {
    color: red;
  }
}}}

Red text.
]]]

Green text again.
```


