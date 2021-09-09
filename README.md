# Specification

This repository contains the specification for the Unimarkup markup language.

The goal of Unimarkup is to combine conventions of other well-known markup languages and combining them to create a markup language that can easily scale from simple README files to scientific papers or full program documentation.

The focus of Unimarkup is

- Usability
- Consistency
- Internationalization
- Flexibility

Since Unimarkup is a markup language, it should be converted to other formats like PDF or HTML. For this, Unimarkup text is first converted to an intermediate representation, and then converted to any of the supported [output formats](Unimarkup_Language_ReferenceManual.md).

Unimarkup works with an implicit type system to provide a more granular control for macros.
See [Unimarkup type system](Unimarkup_Language_ReferenceManual.md).

# Credit

This language was heavily influenced by the Pandoc-Flavor of Markdown, reStructuredText and Latex.

# Terminology

There are several terms used inside the Unimarkup specification that are defined in [Terminology.md](Terminology.md).

# Structure 
## Frontend

The frontend part of Unimarkup defines available Unimarkup elements and how to use them.
The [frontend reference](Frontend_Reference.md) contains the frontend specification.

## Intermediate

The intermediate part of Unimarkup defines how a Unimarkup document is stored in a SQL database.
This part also covers internationalization and localization for Unimarkup documents.
The [intermediate reference](Intermediate_Reference.md) contains the intermediate specification.

## Output format

Different output formats are defined for Unimarkup documents.
The `OutputFormats` folder contains various references on how the intermediate representation is converted to an output format.

# Internationalization and localization

For multi-language support, Unimarkup sets a unique ID for every block element and stores those IDs with the content inside a table of a SQL database.
Other languages are then added as new columns next to the respective entries in the table.

Using the attribute block, it is possible to specify identifiers to blocks of text explicitly. Otherwise, identifiers are added implicitly by Unimarkup.
