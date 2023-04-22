# Namespaces

Every Unimarkup file has its own namespace.
It is either extracted from the `title` [configuration option](/configuration/general-options.md), or the filename if the `title` is not set.
Like the automatic ID generation for [headings](/markup/blocks/heading.md), the namespace is created by setting Latin graphemes to lower case, spaces between graphemes must be replaced by `-`, and other graphemes besides numbers and Latin graphemes must be removed.

The namespace is used to access macros, memorables, and types defined in the file if it is inserted in another file using the [rendered block insert element](/markup/blocks/inserts/render-block-insert.md).


