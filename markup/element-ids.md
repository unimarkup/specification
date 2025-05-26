# Element IDs

**WIP**

**Note:** The ID may not contain `#`, `.`, `+`, `"`, `` ` ``, `'`, or any whitespace.

## Manually set IDs

IDs set manually using element attributes must be taken as is, unless the ID contains invalid graphemes.

To prevent ID conflicts with file inserts, IDs should follow the `<namespace>_<element id>` convention, and the element ID must not contain any `_`.
The implementation should set a warning if this convention is not fulfilled.

## Automatically generated IDs

Element IDs for elements **except** headings and logic elements may be generated automatically by an implementation, but must follow the `<namespace>_<element id>` convention.

The generation of heading IDs is defined in the [heading](/markup/blocks/heading.md) section.
The name of logic elements is used as their ID.
