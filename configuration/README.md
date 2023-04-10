# Configuration

Unimarkup configuration options may be used to customize the rendering behavior of an implementation.
An implementation may provide multiple ways to set those options, but must at least provide the following options:

- CLI ... options may be set as parameters when executing the implementation per CLI
- Preamble ... using the [preamble file decoration](/markup/decorators/preamble)

Configuration options may change depending on the chosen output format, but options that must be available for all formats are defined in the [general options](/configuration/general-options) section.

Options that additionally must be available per CLI are defined in the [CLI](/configuration/cli) section.

The section [merging configurations](/configuration/merging-configurations) defines how two or more configurations must be merged.
This may happen if CLI options and a preamble are set, or other Unimarkup files are inserted.

**Note:** An implementation may provide aliases for configuration options.
