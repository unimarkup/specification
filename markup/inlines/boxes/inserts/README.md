# Inline inserts

Inline inserts may be used to integrate external resources into a Unimarkup file.
The general form for inline inserts looks like a hyperlink with a **keyword** set immediately after `[`.

**Note:** The description given inside `[]` is used as alternative text, if the external resource could not be inserted or displayed. The text may then be used as fallback content for convertible resources, or plain text for media resources.

**Type:** All inline inserts are part of the `inline-insert` type.

There are two different kinds of inline inserts:

1. Media resources

   This refers to resources that cannot be converted to Unimarkup content.
   Examples are images, videos, audio, etc.

   Since the resource is not integrated into the Unimarkup document, it must be assured by the user that the resource is available at the set location.

   The [inline media insert](/markup/inlines/boxes/inserts/inline-media-insert) element may be used to insert media resources as inline content.

2. Convertible resources

   This refers to resources that may be converted to Unimarkup content.
   
   If the resource type is supported by the Unimarkup implementation, the content must be integrated into the Unimarkup document using regular Unimarkup inline elements.
   Since the content is integrated into the Unimarkup document, the resource must only be available for rendering.

   Since the resource must be convertible to Unimarkup, there must be an understanding of a Unimarkup ID in the content of the resource.
   This ID may then be used as **filter attribute** `insert-id` for inserts, to only get the content of the element identified by this ID.

   There are two elements for inline inserts of convertible resources:

   1. [inline render insert](/markup/inlines/boxes/inserts/inline-render-insert)

      This inline element tries to interpret the given content and convert it to fitting Unimarkup inline elements.

      **Note:** If conversion to inline elements is not possible, the alternative text must be used instead. In this case the implementation should set a warning.

   2. [inline verbatim insert](/markup/inlines/boxes/inserts/inline-verbatim-insert)

      This inline element applies verbatim formatting to the content.

      **Note:** If the content contains a blank line, the alternative text must be used instead. In this case the implementation should set a warning.
