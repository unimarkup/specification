# ID referencing

**WIP**

The general syntax for referencing is described in the general [referencing](/markup/inlines/boxes/referencing/README) section.

Every element that allows attributes, may be referenced by its ID using `##` as keyword followed by the `element ID`.
The section [element IDs](/markup/element-ids) describes the concept of element IDs in more detail.

As convenience feature, it must be allowed to reference local elements without setting the namespace part of the element ID.

**Note:** The specification of Unimarkup elements defines if they have a default text. If none is given, the element does not have a default text. 

**Usage:**

```
[!!Some image](<image url>){ "id" : "some-image-id", "ref" : { "label" : "Some image" } }

A paragraph that references [##some-image-id]{ "refOption" : "label" }. 
The referenced text looks like: Some image
```

**Type:** `id-referencing`
