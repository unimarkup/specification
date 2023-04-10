# General options

The following options must be available for all configuration variants.

## Taking values

- `output-file` ... `filepath` that defines the filename (without extension) that must be used for the rendered outputs. The extension of the filename depends on the output format.
                    If no path is given, the output filename(s) may be freely chosen by the implementation.

- `output-formats` ... List of supported output formats the Unimarkup file should be rendered to. Available output formats depend on the used implementation.

- `base` ... `folderpath` that is set before all relative hyperlinks and media inserts.

- `ignore-file` ... File that defines elements and attributes that must be ignored for rendering (The syntax is defined in the [ignore file](/configuration/ignore-file) section)

- `citation-style` ... `filepath` to the citation style sheet that must be used to process referenced literature

- `references` ... `list<filepath>` of one or more reference files in BibTeX or JSON format to use them with literature referencing

- `fonts` ... `list<filepath>` of TTF or WOFF fonts to be able to use them for rendering

- `title` ... `string` to set the title of the rendered document(s)

- `authors` ... `list<string>` to set the authors of the rendered document(s)

- `parameter` ... `list<constant>` to set parameters for a file

  All parameters must have default values and cannot be changed later, making them like [constants](/markup/logic/memorables/constants).

  Parameters must be given in the form:
  
  ```
  <parameter name>: <type> := <default value>
  ```

  **Note:** `: <type>` is optional if the type is defined by the given default value.

## Boolean options

- `overwrite-out-files` ... Overwrite files set with `output-file` if already existing

- `keep-comments` ... Keep comments set in a Unimakup file in the output format.
