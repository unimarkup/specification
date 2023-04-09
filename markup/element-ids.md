# Element IDs

**WIP**

**Note:** The ID may not contain `#`, `.`, `+`, `"`, `` ` ``, or any whitespace.

## Manually set IDs

IDs set manually using element attributes must be taken as is, unless the ID contains invalid graphemes.

To prevent ID conflicts with file inserts, IDs should follow the `<namespace>_<element id>` convention, and the element ID must not contain any `_`.
The implementation should set a warning if this convention is not fulfilled.

## Automatically generated IDs

Element IDs for elements **except** headings and logic elements may be generated automatically by an implementation, but must follow the `<namespace>_<element-type>-<element count of same type from file start>` convention.

The generation of heading IDs is defined in the [heading](/markup/blocks/heading) section.

Logic elements do not have an ID, but are referred to by their name.
However, an implementation may choose to set IDs for logic elements.
This might be useful for the `id` column of the [´.umi` i18n format](/i18n/intermediate-formats/umi/README).

**Example:**

The example assumes `namespace = root`

```
- Bullet list entry 1

  Some paragraph in entry 1.

- Bullet list entry 2

  Some paragraph in entry 2.
```

The above is equivalent to the following manually set IDs:

```
- Bullet list entry 1 { id: "root_bullet-list-entry-1"}

  Some paragraph in entry 1.{ id: "root_paragraph-1"}

- Bullet list entry 2 { id: "root_bullet-list-entry-2"}

  Some paragraph in entry 2.{ id: "root_paragraph-2"}
```
