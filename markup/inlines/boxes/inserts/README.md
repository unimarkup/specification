# Inline inserts

Inline inserts may be used to integrate external resources into a Unimarkup file.
The general form for inline inserts looks like a hyperlink with a **keyword** set immediately after `[`.

**Note:** The description given inside `[]` is used as alternative text, if the external resource could not be inserted or displayed. The text may then be used as fallback content for convertible resources, or plain text for media resources.

**Type:** All inline inserts are subtypes of the `inline-insert` type.

There are two different kinds of inline inserts:

1. Media resources

   This refers to resources that cannot be converted to Unimarkup content.
   Examples are images, videos, audio, etc.

   **Note:** Because the resource may not be integrated into the Unimarkup document, it must be assured by the user that the resource is available at the set location.

   The [inline media insert](/markup/inlines/boxes/inserts/inline-media-insert.md) element may be used to insert media resources as inline content.

2. Convertible resources

   This refers to resources that may be converted to Unimarkup content.

   There are two elements for inline inserts of convertible resources:

   1. [inline render insert](/markup/inlines/boxes/inserts/inline-render-insert.md)

      This inline element tries to interpret the given content and convert it to fitting Unimarkup inline elements.

      **Note:** If conversion to inline elements is not possible, the alternative text must be used instead. In this case, the implementation should set a warning.

      **Note:** Using an empty link is a short way to get rendered inline content, since there is no render formatting.

   2. [inline verbatim insert](/markup/inlines/boxes/inserts/inline-verbatim-insert.md)

      This inline element applies verbatim formatting to the content.

      **Note:** If the content contains a blank line, the alternative text must be used instead. In this case, the implementation should set a warning.
