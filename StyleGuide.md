# General
## Placeholder text

Any verbatim text that is between `<>` is used as placeholder value that may be replaced by any other character sequence.
The `<>` characters are also part of the placeholder value. Placeholder text must start with a lower case letter.

If an element breaks this convention, it must be stated explicitly. 

## Notes

A note is used to highlight information concerning usage restrictions, to prevent wrong usage, or about the rendering behavior of an element.

**Note:** Currently, notes are set by starting a new line with `**Note:**` followed by one space and surrounded by blank lines.\
This might change to `{@note(<Some noteworthy information>)}` after Unimarkup has been implemented.

## List ending

No punctuation must be set if a list entry consists only of one sentence. Otherwise, a punctuation must be set at the end of this list entry.

# Naming conventions

For better consistency and readability, the following naming conventions are used in this specification.

## Macro naming

Macro names should be verbs and must be written in [**camelCase**](https://en.wikipedia.org/wiki/Camel_case).
The name must start with a Latin character or `_`.
Macros starting with `_` mark a private macro.
The remaining name may consist of Latin characters, digits and `_`.

**Example:**

```
{@renderSomething}

{@_privateMacro}
```

## Variable naming

Variable names must be written in [**camelCase**](https://en.wikipedia.org/wiki/Camel_case).
If a variable is used as a constant, the name must be written in [**SCREAMING_SNAKE_CASE](https://en.wikipedia.org/wiki/SCREAMING_SNAKE_CASE). The name must start with a Latin character or `_`.
Variables starting with `_` mark a private variable.
The remaining name may consist of Latin characters, digits and `_`.

**Example:**

```
{%someVariable}

{%CONSTANT_VARIABLE}
```

## Attribute naming

Attribute names and none numerical values of attributes must be written in [**lower-kebab-case**](https://en.wikipedia.org/wiki/Kebab_case). The name must start with a Latin character.
The remaining name may consist of Latin characters, digits and `-`.

**Example:**

```json
{ "some-attribute" : "some-value" }

{ "some-numerical-attribute" : 2 }
```

## Element naming

Element names should always be in singular form and must only consist of words with Latin characters.

**Example:**

```
Bullet list

Render block
```

## Type naming

Type names must be written in [**PascalCase**](https://en.wikipedia.org/wiki/PascalCase).
The name of element types should reflect the element name and must only consist of Latin characters, digits and `_`.

**Example:**

```
Paragraph

BlockQuotation

BulletList
```
