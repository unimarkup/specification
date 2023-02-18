# Glossary for the Unimarkup specification

The following terms are ordered so that later terms may build upon earlier ones.

## Grapheme

A grapheme in Unimarkup is a [Unicode grapheme](https://www.unicode.org/glossary/#grapheme).

## Grapheme sequence

A sequence of one or more graphemes is called grapheme sequence.

## Whitespace

A whitespace in Unimarkup is any Unicode code point marked with ["WSpace=Y" or "WS"](https://en.wikipedia.org/wiki/Whitespace_character#Unicode).

## Space

One space in Unimarkup is one [Unicode space](https://util.unicode.org/UnicodeJsps/character.jsp?a=0020) `U+0020`.

## Line break

Any grapheme sequence that forces a new line, is treated as a line break.

## Line

A line is a sequence of graphemes that ends with a [line break](#line-break).

## Empty line

A line is considered empty if it only consists of whitespaces.

## Blank line

A blank line consists of one or more subsequent empty lines.

**Note:** Multiple blank lines are treated as one blank line.

## Content

A content describes any grapheme sequence.

## Rendering

Rendering is the process to convert Unimarkup content into any of the available output formats.

## Keyword

A keyword consists of one or more special grapheme sequences used to identify Unimarkup markup.

## Element

A Unimarkup element consists of content, and keywords that define how the content gets rendered.

## Element group

An element group groups Unimarkup elements that have a similar syntax and/or restrictions.

## Root input

The root input contains Unimarkup markup, and is the single entry point to get a rendered output.

## Document

A document is the ordered list of Unimarkup elements that is retrieved by parsing the root input.

## Document flow

A document flows from the highest point of the document, which is the first line of the root input, to the lowest point of the document, which is the last line of the root input.

**Note:** Above refers to content that is closer to the highest point compared to the current one.

**Note:** Below refers to content that is closer to the lowest point compared to the current one.

## Heading height

There are six heading levels ranging from 1 to 6. The heading at level 1 is considered as the highest level and 6 as the lowest.

## Section

A section refers to the content between two headings.

**Note:** The next section refers to section that is at least at the same heading level or higher.

**Note:** Next sections refers to two or more sections that are below the current section.

## Verbatim text

A verbatim text is a sequence of characters that is taken as is without any interpretation of those characters.

## List entry

A list entry is one element of a list element.
