# Line break

A line break is set with three or more `:`.
If it is not inside an enclosed element, it must be treated like a page break.
How a page break is rendered may depend on the output format.

Enclosed elements may change the behavior of a line break.
In this case, the behavior must be defined in the description line of the enclosed element.
If the element does not define a custom behavior, the line break must be treated like a page break.

Attributes may be set directly after the last `:`.
These attributes must only affect the line break itself.

**Usage:**

```
Page 1

:::

Page 2
```

**Type:** `line-break`
