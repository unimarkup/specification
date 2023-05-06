# General options

The following options must be available for all configuration variants.

## Taking values

- `output-file` ... `filepath` that defines the filename (without extension) that must be used for the rendered outputs. The extension of the filename depends on the output format.
                    If no path is given, the output filename(s) may be freely chosen by the implementation.

- `output-formats` ... List of supported output formats the Unimarkup file should be rendered to. Available output formats depend on the used implementation.

- `base` ... `folderpath` that is set before all relative hyperlinks and media inserts.

  **Note:** This path is not used for path lookup during rendering.

- `ignore-file` ... File that defines elements and attributes that must be ignored for rendering (The syntax is defined in the [ignore file](/configuration/ignore-file.md) section)

- `citation-style` ... `filepath` to the citation style sheet that must be used to process referenced literature

- `references` ... `list<filepath>` of one or more reference files in BibTeX or JSON format to use them with literature referencing

- `fonts` ... `list<filepath>` of TTF or WOFF fonts to be able to use them for rendering

- `title` ... `inline` to set the title of the rendered document(s)

- `authors` ... `list<inline>` to set the authors of the rendered document(s)

- `description` ... `inline` to provide a short description about the file

- `parameter` ... `list<constant>` to set parameters for a file

  All parameters must have default values and cannot be changed later, making them like [constants](/markup/logic/memorables/constants.md).

  Parameters must be given in the form:
  
  ```
  <parameter name>: <type> := <default value>
  ```

  **Note:** `: <type>` is optional if the type is defined by the given default value.

## Boolean options

- `overwrite-out-files` ... Overwrite files set with `output-file` if already existing

- `keep-comments` ... Keep comments set in a Unimakup file in the output format.

- `allow-unsafe` ... Allows unsafe features like JavaScript, WebAssembly, etc.

  **Note:** This option must not have any effect if an `ignore-file` is set.

  **Note:** An implementation is free to define what features are considered unsafe.
