# Introduction

This document is the specification for the middle end part of the Unimarkup markup language.
The middle end part is an intermediate form that helps to decouple frontend parsing and backend rendering
and also opens up the possibility to introduce a multi-language concept for Unimarkup.

# Intermediate tables

The intermediate form is a SQL database consisting of five tables storing information about one Unimarkup file.
This Unimarkup file is referred to as **root** in all further sections.

- **Content**

  This is the main table, storing all used Unimarkup block elements with their content of the root Unimarkup file as rows, except used Variables and Macros.
  See [content table](#content-table) for more details.

- **Variables**

  This table stores all variables that are used in the root Unimarkup file.
  See [variables table](#variables-table) for more details.

- **Macros**

  This table stores all macros that are used in the root Unimarkup file.
  See [macros table](#macros-table) for more details.

- **Metadata**

  This table stores metadata information about the root Unimarkup file and all Unimarkup files that are rendered and/or inserted into the root Unimarkup file.
  See [metadata table](#metadata-table) for more details.

- **Resources**

  This table stores all paths to externally referenced files that are used inside the root Unimarkup file and can not be converted to Unimarkup elements.
	See [resource table](#resource-table) for more details.

## Content table

The content table stores all used Unimarkup block elements of the root Unimarkup file as rows, except used Variables and Macros.
Block elements that allow nesting are split into multiple rows depending on their inner type for the identification of nested block elements.

The table consists of the following columns:

- `id` ...--not null text-- The ID of the stored block element that is either set explicitly, or implicitly while parsing
- `type` ...--not null text-- The type of the stored block element
- `text` ...--text-- The text of the block element or parts of it, if the block has nested block elements
- `fallback-text` ...--not null text-- This text field is used if the `text` field is empty, which can happen in multi-language context
- `attributes` ...--text-- Unformatted JSON attributes for the stored block element (The first and last character must be `{}` to enclose JSON data)
- `fallback-attributes` ...--not null text-- This field is used if the `attributes` field is empty, which can happen in multi-language context
- `line-nr` ...--not null bigint-- The line number of the parsed Unimarkup file where the block element starts

The primary key for this table is the combination of `id` and `line-nr`.

**Type extension:** 

Block elements have an additional `<typename>_open` and `<typename>_close` type, where `typename` denotes the type of the block element.

## Variables table

The variable table stores all variables that are used inside the root Unimarkup file.

The table consists of the following columns:

- `name` ...--not null text-- The name of the variable
- `type` ...--not null text-- The type of the variable
- `value` ...--text-- The value of the variable

The primary key for this table is the `name` field. This means, that a variable is unique by its `name` independent of its type.

## Macros table

The macros table stores all macros that are used inside the root Unimarkup file.

The table consists of the following columns:

- `name` ...--not null text-- The name of the macro
- `type` ...--not null text-- The type of the macro
- `parameters` ...--text-- The parameters of the macro
- `body` ...--text-- The body of the macro

The primary key for this table is the combination of `name` and `parameters`. This means, that a macro is unique by its `name` and `parameters`.

## Metadata table

The metadata table contains metadata about the root Unimarkup file and all Unimarkup files that are rendered or inserted inside the root Unimarkup file.

The table consists of the following columns:

- `filename` ...--not null text-- The name of a Unimarkup file
- `filehash` ...--not null binary-- The sha256 hash of the file set at `filename`
- `path` ...--not null text-- The path including the `filename`, where the file is located
- `preamble` ...--text-- The unformatted JSON or YAML preamble of the file set at `filename`. If this field starts with `{`, JSON is assumed and the field must end with `}`. Otherwise, YAML is used for parsing
- `root` ...--not null bit-- This field defines if the `filename` is the root of the Unimarkup document with `root = True`. Otherwise, `filename` refers to an Unimarkup file that is rendered and/or inserted in the root Unimarkup file

The primary key for this table is the `filehash` field.

## Resource table

The resource table contains files that are rendered and/or inserted in the root Unimarkup file that can not be converted to Unimarkup elements.
Files that can not be converted to Unimarkup elements are for example images and videos of any format.

The table consists of the following columns:

- `filename` ...--not null text-- The name of a resource file
- `path` ...--not null text-- The path including the `filename`, where the file is located

The primary key for this table is the `path` field.


# Multi-language handling

;;mhatzl;;


