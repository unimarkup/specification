# Introduction

This document is the specification for the middle end part of the Unimarkup markup language.
The middle end part is an intermediate form that helps to decouple frontend parsing and backend rendering
and also opens up the possibility to introduce a multi-language concept for Unimarkup.

# Intermediate tables

The intermediate form is a SQL database consisting of several tables storing information about one Unimarkup file.
This Unimarkup file is referred to as **root** in all further sections.

- **Content**

  This is the main table, storing all used Unimarkup block elements with their content of the root Unimarkup file as rows, except used Variables and Macros.
  See [content table](#content-table) for more details.

- **Variables**

  This table stores all variables that are defined for the Unimarkup document.
  See [variable table](#variable-table) for more details.

- **Macros**

  This table stores all macros that are defined for the Unimarkup document.
  See [macro table](#macro-table) for more details.

- **Metadata**

  This table stores metadata information about the root Unimarkup file and all Unimarkup files that are rendered and/or inserted into the root Unimarkup file.
  See [metadata table](#metadata-table) for more details.

- **Resources**

  This table stores all paths to externally referenced files that are used inside the root Unimarkup file and can not be converted to Unimarkup elements.
	See [resource table](#resource-table) for more details.

- **Abbreviations**

  This table stores all abbreviations, that are defined for the Unimarkup document.
  See [abbreviation table](#abbreviation-table) for more details.

- **Footnotes**

  This table stores all footnotes, that are defined for the Unimarkup document.
  See [footnote table](#footnote-table) for more details.

- **Endnotes**

  This table stores all endnotes, that are defined for the Unimarkup document.
  See [endnote table](#endnote-table) for more details.

- **Literature**

  This table stores all literature, that are defined for the Unimarkup document.
  See [literature table](#literature-table) for more details.

## Content table

The content table stores all used Unimarkup block elements of the root Unimarkup file as rows, except used Variables and Macros.
Block elements that allow nesting are split into multiple rows depending on their inner type for the identification of nested block elements.

The table consists of the following columns:

- `id` ...--not null text-- The ID of the stored block element that is either set explicitly, or implicitly while parsing
- `um_type` ...--not null text-- The Unimarkup type of the stored block element
- `text` ...--text-- The text of the block element or parts of it, if the block has nested block elements
- `fallback-text` ...--text-- This text field is used if the `text` field is empty, which can happen in multi-language context
- `attributes` ...--text-- Unformatted JSON attributes for the stored block element (The first and last character must be `{}` to enclose JSON data)
- `fallback-attributes` ...--text-- This field is used if the `attributes` field is empty, which can happen in multi-language context
- `line-nr` ...--not null bigint-- The line number of the parsed Unimarkup file where the block element starts

The primary key for this table is the combination of `id` and `line-nr`.

**Type extension:** 

Block elements have an additional `<typename>_open` and `<typename>_close` type, where `typename` denotes the type of the block element.

## Variable table

The variable table stores all variables that are defined for the Unimarkup document.

The table consists of the following columns:

- `name` ...--not null text-- The name of the variable
- `um_type` ...--not null text-- The Unimarkup type of the variable
- `context` ...--not null text-- The context defines usage restrictions for variables
- `value` ...--text-- The value of the variable
- `fallback-value` ...--text-- The value of the variable that is used if `variable` is empty, which can happen in multi-language context

The primary key for this table is the `name` field. This means, that a variable is unique by its `name` independent of its type.

The context can be set to `all` to have no restriction, to a specific macro or combination of macros, to only allow a variable to be used inside certain macros, or to any Unimarkup type or combination of types, to only allow the usage inside certain Unimarkup elements. The combination of macros and types is given in the form `({@<first-macroname>}|{@<second-macroname>})` or `(<first-type>|<second-type>)`.

## Macro table

The macro table stores all macros that are defined for the Unimarkup document.

The table consists of the following columns:

- `name` ...--not null text-- The name of the macro
- `um_type` ...--not null text-- The Unimarkup type of the macro
- `context` ...--not null text-- The context defines usage restrictions for macros
- `parameters` ...--text-- The parameters of the macro
- `body` ...--text-- The body of the macro
- `fallback-body` ...--text-- The body of the macro that is used if `body` is empty, which can happen in multi-language context

The primary key for this table is the combination of `name` and `parameters`. This means, that a macro is unique by its `name` and `parameters`.

The context can be set to `all` to have no restriction, to a specific macro or combination of macros, to only allow a macro to be used inside certain macros, or to any Unimarkup type or combination of types, to only allow the usage inside certain Unimarkup elements. The combination of macros and types is given in the form `({@<first-macroname>}|{@<second-macroname>})` or `(<first-type>|<second-type>)`.

## Metadata table

The metadata table contains metadata about the root Unimarkup file and all Unimarkup files that are rendered or inserted inside the root Unimarkup file.

The table consists of the following columns:

- `filename` ...--not null text-- The name of a Unimarkup file
- `filehash` ...--not null blob-- The sha256 hash of the file set at `filename`
- `path` ...--not null text-- The path including the `filename`, where the file is located
- `preamble` ...--text-- The unformatted JSON or YAML preamble of the file set at `filename`. If this field starts with `{`, JSON is assumed and the field must end with `}`. Otherwise, YAML is used for parsing
- `fallback-preamble` ...--text-- This preamble is used if `preamble` is empty, which can happen in multi-language context
- `root` ...--not null bit-- This field defines if the `filename` is the root of the Unimarkup document with `root = True`. Otherwise, `filename` refers to an Unimarkup file that is rendered and/or inserted in the root Unimarkup file

The primary key for this table is the `filehash` field.

## Resource table

The resource table contains files that are rendered and/or inserted in the root Unimarkup file that can not be converted to Unimarkup elements.
Files that can not be converted to Unimarkup elements are for example images and videos of any format.

The table consists of the following columns:

- `filename` ...--not null text-- The name of a resource file
- `path` ...--not null text-- The path including the `filename`, where the file is located

The primary key for this table is the `path` field.

## Abbreviation table

The abbreviation table stores all abbreviations that are defined for the Unimarkup document.

The table consists of the following columns:

- `abbreviation` ...--not null text-- The name of the abbreviation
- `content` ...--text-- The content of the abbreviation
- `fallback-content` ...--text-- The content of the abbreviation that is used if `content` is empty, which can happen in multi-language context

The primary key for this table is the `abbreviation` field.

## Footnote table

The footnote table stores all footnotes that are defined for the Unimarkup document.

The table consists of the following columns:

- `id` ...--not null text-- The ID of the footnote
- `content` ...--text-- The content of the footnote
- `fallback-content` ...--text-- The content of the footnote that is used if `content` is empty, which can happen in multi-language context

The primary key for this table is the `id` field.

## Endnote table

The endnote table stores all endnotes that are defined for the Unimarkup document.

The table consists of the following columns:

- `id` ...--not null text-- The ID of the endnote
- `content` ...--text-- The content of the endnote
- `fallback-content` ...--text-- The content of the endnote that is used if `content` is empty, which can happen in multi-language context

The primary key for this table is the `id` field.

## Literature table

The Literature table stores all literature that is defined for the Unimarkup document.

The table consists of the following columns:

- `id` ...--not null text-- The ID of the literature
- `data` ...--text-- The data of the literature being given in JSON form
- `fallback-data` ...--text-- The data of the literature that is used if `data` is empty, which can happen in multi-language context

The primary key for this table is the `id` field.

# Multi-language handling
## Steps **before** content translation

Since the intermediate tables have fixed columns for better database modelling inside programming languages, the intermediate database must be exported. 
This can be done by setting `intermediate` as output format in the preamble.

To add another language, new columns must be added for each table column that supports a corresponding fallback column,
where the column name defines the language and content that is expected by Unimarkup.
The language must be given in the [IETF BCP 47 language tag](https://tools.ietf.org/rfc/bcp/bcp47.txt) format.

**Note:** The language tag set in the preamble of the `intermediate` output format is prepended for all columns of the exported database that have a corresponding fallback column.

- New columns inside the content table
  - `<language tag>-text` ...--text-- Contains the text of a block element entry in the language set as `<language tag>`
  - `<language tag>-attributes` ...--text-- Contains the attributes of a block element entry in the language set as `<language tag>`

- New columns inside the variables table
  - `<language tag>-value` ...--text-- Contains the value of a variable entry in the language set as `<language tag>`
  
- New columns inside the macros table
  - `<language tag>-body` ...--text-- Contains the body of a macro entry in the language set as `<language tag>`

- New columns inside the metadata table
  - `<language tag>-preamble` ...--text-- Contains the preamble of a Unimarkup file entry in the language set as `<language tag>`

## Steps **after** content translation

The modified database can now be used instead of a Unimarkup file to generate outputs defined in the preamble of the root entry of the metadata table.
Two language tags must be set when executing Unimarkup, where one is used as default and the other one as fallback language.

**Note:** Internally, the given database entries are copied to the internal database with the two languages being mapped to the default and fallback columns.
