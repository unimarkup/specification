
# Unimarkup configuration

A configuration can be set per Unimarkup document, that defines several options, including the output formats that should be rendered.
The configuration can be set either per [CLI](#configuration-per-cli), per [preamble](Frontend_Reference.md#preamble), or by creating a `config.json` or `config.yaml` file inside a directory that is set with the environmental variable `UNIMARKUP_CONFIG`. 
The environmental variable will per default point to a `.unimarkup` directory in the current working directory. 

## General options

The following options are available for all configuration variants.

### Taking values

- `output-file` ...--`filepath`-- Defines the filename (without extension) that must be used for the rendered outputs. The extension of the filename depends on the output format.
                    If no path is given, the output file(s) will be rendered into the workspace folder.

- `output-formats` ... Set output formats the Unimarkup document should be rendered to. Set outputs are also treated as flags inside the Unimarkup document. ;; mhatzl: link to possible formats

- `insert-paths` ...--`list<folderpath>`-- Set paths that are searched for relative file and image inserts.

- `dot-unimarkup` ...--`folderpath`-- Set the path to a directory that is used for default configuration and theme settings. The intermediate form of rendered documents will also be stored at this path.

- `theme` ...--`filepath`-- Set a Unimarkup theme file to be used for rendering.

- `flag` ...--`list<string>`-- Set flags that will be set for rendering.

- `enable-elements` ...--`list<Unimarkup block elements>`-- Explicitly set Unimarkup block elements that can be used inside the given Unimarkup document. If this option is set, all Unimarkup elements that are not given are disabled.

- `disable-elements` ...--`list<Unimarkup block elements>`-- Explicitly set Unimarkup block elements that can NOT be used inside the given Unimarkup document. If this option is set, all Unimarkup elements that are not given are enabled.

- `citation-style` ...--`filepath`-- Set citation style sheet that is used to process referenced literature.

- `references` ...--`list<filepath>`-- Set one or more reference files in BibTeX or JSON format to use them with literature referencing.

- `fonts` ...--`list<filepath>`-- Set TTF or WOFF fonts to be able to use them for rendering.

### Boolean options

- `overwrite-out-files` ... Overwrite files set with `out-file` if already existing.

- `clean` ... Deletes all previously rendered documents stored inside the `dot-unimarkup` path.

- `rebuild` ... Ignores all previously rendered documents stored inside the `dot-unimarkup` path and renders the given Unimarkup file.

- `relative-insert-prefix` ... This prefix will be set before inserts in the rendered document to inserts that use relative paths. **Note:** During rendering, the original relative path is taken.

## HTML options
### Taking values

- `html-template` ...--`filepath`-- Set a template HTML file with `{{ head }}` set inside the `head` element and `{{ body }}` set inside the body element.
                      Styling, fonts and scripts will be inserted at `{{ head }}` and the rendered Unimarkup content is placed inside `{{ body }}`.
                      Optionally, `{{ toc }}` can be set to get the table of contents (**Note:** This will not remove a rendered table of contents inside the rendered Unimarkup content if present).

- `html-mathmode` ...--`(svg|embed|cdn)`-- Set the mathmode of MathJax to be used for rendered HTML documents.

### Boolean options

- `html-embed-svg` ... Set if svgs should be embedded into html instead of inserted as regular images.

# Configuration per CLI

Unimarkup configurations set as command line arguments take the highest precedence over all configuration options.

In addition to the options that are valid for all configuration options, additional options are available.

### Taking values

- `um-file` ...--`filepath`-- The filename of the Unimarkup file that is used as root for rendering. **Note:** This is a mandatory setting to identify the Unimarkup file that should be rendered.
                It can either point to a `.um` file, or `.db` that contains the intermediate representation.

### Boolean options

- `replace-preamble` ... Set if preamble of given Unimarkup file is replaced with the given arguments. If not set, given arguments overwrite the corresponding preamble settings, but other settings are still used.

