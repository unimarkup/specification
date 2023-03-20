# Configuration

This section contains configuration properties that are specific to internationalization.

**WIP**


## Taking values

- `lang` ... [bcp47](https://www.rfc-editor.org/rfc/bcp/bcp47.txt) code for the default language the Unimarkup content is written in

- `langs` ... `list<bcp47-code>` of languages to create outputs for

  **Note:** If the output is to an intermediate format, the given languages may define the number of language columns that are initially created.

  **Note:** If the output is to a regular output format, the given input file must be of an intermediate format, and this file must contain content for all set languages. Otherwise, the output cannot be created for all languages.

- `output-formats` ... in addition to the regular output formats, intermediate formats may also be set as outputs

- `input-file` ... in addition to the regular Unimarkup file, all supported intermediate formats may be used for an input file

## Boolean options

