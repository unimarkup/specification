# Block inserts

Block inserts may be used to integrate external resources into a Unimarkup file.
The general form for block inserts looks like a hyperlink with a **keyword** set directly before `[`.

**Note:** The description given inside `[]` is used as alternative text, if the external resource could not be inserted or displayed. The text may then be used as fallback content for convertible resources, or plain text for media resources.

**Type:** All block inserts are part of the `block-insert` type.

There are two different kinds of block inserts:

1. Media resources

   This refers to resources that cannot be converted to Unimarkup content.
   Examples are images, videos, audio, etc.

   Since the resource is not integrated into the Unimarkup document, it must be assured by the user that the resource is available at the set location.

   The [block media insert](/markup/blocks/inserts/media-block-insert) element may be used to insert media resources as block content.

2. Convertible resources

   This refers to resources that may be converted to Unimarkup content.
   
   If the resource type is supported by the Unimarkup implementation, the content must be integrated into the Unimarkup document using regular Unimarkup block elements.
   Since the content is integrated into the Unimarkup document, the resource must only be available for rendering.

   Since the resource must be convertible to Unimarkup, there must be an understanding of a Unimarkup ID in the content of the resource.
   One or more Unimarkup IDs may then be used as **filter attribute** `insert-ids` for inserts, to only get the content of the elements identified by the given IDs.

   **Note:** Multiple IDs must be separated by whitespace.

   **Note:** The order of inserted elements must follow the document flow of the external resource.

   There are two elements for block inserts of convertible resources:

   1. [block render insert](/markup/blocks/inserts/render-block-insert)

      This block element tries to interpret the given content and convert it to fitting Unimarkup block elements.

      **Note:** If conversion to block elements is not possible, the alternative text must be used instead. In this case, the implementation should set a warning if the link was not empty.

   2. [block verbatim insert](/markup/blocks/inserts/verbatim-block-insert)

      This block element applies verbatim formatting to the content.
