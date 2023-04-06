# ID referencing

**WIP**

The general syntax for referencing is described in the general [referencing](/markup/inlines/boxes/referencing/README) section.

Every element that allows attributes, may be referenced by its ID using `##` as keyword followed by the `element ID`.
The section [element IDs](/markup/element-ids) describes the concept of element IDs in more detail.

As convenience feature, it must be allowed to reference local elements without setting the namespace part of the element ID.

**Note:** Some Unimarkup elements may have a default text that should be shown when referenced. If no default text is set, one must be set explicitly after the ID using `:` to separate ID and text. 

**Note:** The reference text of an element may be overridden even for elements that have a default text.

**Usage:**

- **Element with default text**

  ```
  [!!Some image](<image url>){ id: "some-image-id" }

  A paragraph that references [##some-image-id].
  ```

  **Note:** The referenced text looks like: `Some image`

- **Element without default text**

  ```
  [Some text]{ id: "some-id" }

  Referencing [##some-id: some text box].
  ```

  **Note:** The referenced text looks like: `some text box`

**Type:** `id-referencing`
