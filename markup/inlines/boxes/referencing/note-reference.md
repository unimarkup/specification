# Note referencing

Notes may be used to reference additional content that should not be part of the normal document flow.

A note may be referenced with `[^^<note-id>]`.

**Note:** A note does not have a default text, so at least one reference of the ID must set a custom text. The first note reference in the document flow with custom text is then used for all references without a custom text.

**Note:** IDs have the same restrictions as manually set IDs for [elements](/markup/element-ids.md).

**Note:** Note IDs of other files that are part of the document may be referenced by setting `<namespace of the file>_<note ID>`. 

## Displaying notes

Note text must not be displayed where they are referenced.

**TODO:** A macro to render referenced notes must be available.
