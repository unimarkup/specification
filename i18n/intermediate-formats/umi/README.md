# `.umi` intermediate format

This intermediate format is an open document spreadsheet with a specific column layout.
A block element, or any Unimarkup element surrounded by blank lines, is stored as one or more rows. The number of rows depends on the element.

**Note:** Inline markup is kept as is to make sentences more readable.

The format specification is split into the following sections:

- [Column layout](#column-layout) ... Defines the overall file structure
- [Blocks](/i18n/intermediate-formats/umi/blocks/README) ... Defines how block elements must be stored in a `.umi` file
- [Logic](/i18n/intermediate-formats/umi/logic/README) ... Defines how logic elements must be stored in a `.umi` file
- [Decorators](/i18n/intermediate-formats/umi/decorators) ... Defines how decorators must be stored in a `.umi` file

## Column layout

**WIP**

- `id` ... The ID of the stored element that is either set explicitly, or implicitly while parsing
- `kind` ... The Unimarkup element kind of the stored element
- `content-<bcp47 lang>` ... The content of the element or parts of it if the element has nested content. The locale of the content is set per [bcp47 language tag](https://www.rfc-editor.org/rfc/bcp/bcp47.txt).
- `attributes-<bcp47 lang>` ... Attributes for the stored element in the set locale
- `position` ... The position of the Unimarkup element in document flow, with the preamble starting at `position = 0`

**Note:** The column names must be set in the first row, marking it as header row.

**Note:** It is possible to add content and attribute columns with other bcp47 language tags to existing `.umi` files to translate the original content to other languages. 

Set bcp47 tags of the [language configuration properties](/i18n/configuration/README) are then searched in the `.umi` headers `content` and `attribute` columns.
