# Merging configurations

This section defines how general configuration options must be merged.
For merging, the configuration that was set first, when starting execution,
is referred to as `main`, and all others as `additionals`.

## Taking values

- `output-file` ... Use setting from `main` if set, or the first `additional` that sets this option
- `output-formats` ... Use setting from `main` if set, or the first `additional` that sets this option
- `base` ... Use setting from `main` if set, or from the preamble of the root file. Otherwise, ignore this setting.
- `ignore-file` ... Merge the content of all found ignore-files, but only include `!` inverted rules from the first found ignore-file
- `citation-style` ... Use setting from `main` if set, or the first `additional` that sets this option
- `references` ... Merge references of all configurations
- `fonts` ... Merge fonts of all configurations
- `title` ... Use setting from `main` if set, or the first `additional` that sets this option
- `authors` ... Merge authors of all configurations
- `description` ... Use the setting from `main`, or the `root` file
- `parameters` ... Merge given parameters, but take `main` parameters if a name collision would occur

## Boolean options

Only consider `main` options for all boolean options.
