# CLI options

The following configuration options must be available per CLI.

## Taking values

- `input-file` ... `filepath` to the Unimarkup file that must be used as root for rendering

  **Note:** This is a mandatory setting to identify the Unimarkup file that should be rendered.

  **Note:** Implementations may choose to get this option via a positional argument rather than by name.

## Boolean options

- `ignore-preamble` ... Set to `true` to only consider the options set per CLI 
