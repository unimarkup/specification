# Specification

This repository contains the specification for the Unimarkup markup language.

The goal of Unimarkup is to combine conventions of other well-known markup languages, and create a markup language that can easily scale from simple README files to scientific papers, and full program documentation.

The focus of Unimarkup is

- Usability
- Consistency
- Internationalization

Since Unimarkup is a markup language, the content will mostly be converted to other formats like PDF or HTML as defined in the [output-formats](output-formats/README) folder.
Besides those more final formats, the [i18n](i18n/README) folder defines intermediate formats to help with content localization.

Unimarkup also integrates a more programming language like markup that is defined in the [markup/logic](/markup/logic/README) folder.
This makes the construction of more complex content easier, and improves content reusability.

# Example

The following example uses some Unimarkup elements.
Detailed description about those elements, and others may be found in the [markup](markup/README) section. 

```
# Heading
## Sub-Heading

Some pragraph inside the sub-heading section.
Common **inline** ||markup|| that *all*ows ***inner* word** and `nesting`. 

## Escaping, links, references and text-box

Escape any character using a single backslash.
Also inside `verbatim \` text`.

[links](uri) should look familiar if you know Markdown.

Reference [##unimarkup-elements], [^^notes], or [&&literature].

Use a [text-box]{ color : red } to apply additional styling.

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

This language was inspired by many other markup and programming languages.

Other great markup languages (given in alphabetical order):

- [AsciiDoc](https://asciidoc.org/)
- [CommonMark](https://commonmark.org/)
- [HTML](https://www.w3.org/html/)
- [LaTeX](https://www.latex-project.org/)
- [Markdown by John Gruber](https://daringfireball.net/projects/markdown/)
- [Pandoc-Flavor of Markdown](https://pandoc.org/MANUAL.html)
- [reStructuredText](https://docutils.sourceforge.io/rst.html)

# Structure 

The following structure of the Unimarkup specification is given in alphabetical order.

- [addons](addons/README) ... contains language addons that are not part of the core specification
- [configuration](configuration/README) ... contains the configuration options for Unimarkup files that must be supported by Unimarkup implementations
- [glossary](glossary) ... contains definitions for terms used in the Unimarkup specification
- [i18n](i18n/README) ... contains internationalization aspects of the Unimarkup specification that must be supported by Unimarkup implementations
- [markup](markup/README) ... contains the core markup syntax for the Unimarkup language
- [output-formats](output-formats/README) ... contains the output formats that must be supported by Unimarkup implementations, and defines the conversion from Unimarkup markup to the output format 

# Specification notes
## Placeholder text

Any verbatim text that is between `<>` is used as placeholder value that may be replaced by any other text.
The `<>` graphemes are also part of the placeholder value.

If an element breaks this convention, it must be stated explicitly.

## Notes

A note is used to highlight information concerning usage restrictions, to prevent wrong usage, or about the rendering behavior of an element.

**Note:** Notes are set by starting a new line with `**Note:**` followed by one space and surrounded by blank lines.

# License

<a rel="license" href="http://creativecommons.org/licenses/by-nd/4.0/"><img alt="Creative Commons License" style="border-width:0" src="https://i.creativecommons.org/l/by-nd/4.0/88x31.png" /></a><br />This work is licensed under a <a rel="license" href="http://creativecommons.org/licenses/by-nd/4.0/">Creative Commons Attribution-NoDerivatives 4.0 International License</a>.

**Short explanation:** The *No Derivatives* part should help to encourage people to get involved in improving the core specification, rather than spin-off their own variation.
