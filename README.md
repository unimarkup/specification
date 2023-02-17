# Specification

This repository contains the specification for the Unimarkup markup language.

The goal of Unimarkup is to combine conventions of other well-known markup languages, and create a markup language that can easily scale from simple README files to scientific papers and full program documentation.

The focus of Unimarkup is

- Usability
- Consistency
- Internationalization
- Flexibility

Since Unimarkup is a markup language, it should be converted to other formats like PDF or HTML. For this, Unimarkup text is first converted to an intermediate representation, and then converted to any of the supported [output formats](Unimarkup_Language_ReferenceManual.md).

Unimarkup works with an implicit type system to provide a more granular control for macros.
See [Unimarkup type system](TypeSystem.md).

# Example

The following example uses some Unimarkup elements.
Detailed description about those elements, and others may be found under the [Frontend](Frontend/) section. 

```
# Heading
## Sub-Heading

Some pragraph inside the sub-heading section.
Common **inline** ||markup|| that *all*ows ***inner* word** and `nesting`. 

## Escaping, links, references and text groups

Escape any character using a single backslash.
Also inside `verbatim \` text`.

[links](uri) should look familiar.

Reference [##unimarkup-elements], [^^notes], or [&&literature].

Use [text groups]{ "color":"red" } to apply additional styling.

# Blocks

|||

First column with a task list:

-[] Main task (still open)
  -[x] Completed sub-task
  -[ ] Remaining task

:::

Second column with a table:

===
| column 1 row 1 | column 2 row 1 |
| column 2 row 2 | column 2 row 2 |
===

|||
```

# Credit

This language was heavily influenced by the Pandoc-Flavor of Markdown, reStructuredText and Latex.

# Terminology

There are several terms used inside the Unimarkup specification that are defined in [Terminology.md](Terminology.md).

# Structure 
## Frontend

The frontend part of Unimarkup defines available elements and constructs in Unimarkup, and how to use them.
The [frontend reference directory](Frontend/README.md) contains the frontend specification.

## Middle end

The middle end part of Unimarkup defines how a Unimarkup document is stored in an intermediate representation.
This part also covers multi-language support for Unimarkup documents.
The [middle end reference](Middleend_Reference.md) contains the middle end specification.

## Output format

Different output formats are defined for Unimarkup documents.
The `OutputFormats` folder contains various references on how the intermediate representation is converted to an output format.

# Internationalization and localization
## Multi-language

For multi-language support, Unimarkup sets a unique ID for every block element and stores those block elements with their IDs inside a table that can be exported.
Other languages can then be added as new columns next to the respective entries in the table and replace the text on block element level.
For more details, read the [multi-language section](Middleend_Reference.md#multi-language) inside the middle end reference.

Using the attribute block, it is possible to specify identifiers for block elements explicitly. Otherwise, identifiers are added implicitly by Unimarkup.

## Localization

In addition to the multi-language concept, [variables](Frontend/Variables.md) and [macros](Frontend/Macros.md)
may be used to add localization capabilities.


# License

<a rel="license" href="http://creativecommons.org/licenses/by-nd/4.0/"><img alt="Creative Commons License" style="border-width:0" src="https://i.creativecommons.org/l/by-nd/4.0/88x31.png" /></a><br />This work is licensed under a <a rel="license" href="http://creativecommons.org/licenses/by-nd/4.0/">Creative Commons Attribution-NoDerivatives 4.0 International License</a>.

**Short explanation:** The *No Derivatives* part should help to encourage people to get involved in improving the core specification, rather than spin-off their own variation.
