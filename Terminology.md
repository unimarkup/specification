# Character

A character in Unimarkup is considered as one [Unicode glyph](https://www.unicode.org/glossary/#glyph).

White-space characters are all Unicode characters marked with ["WSpace=Y" or "WS"](https://en.wikipedia.org/wiki/Whitespace_character#Unicode).

All characters that are not white-space characters are treated as none-white-space characters.

Digit characters are all Unicode code points from `U+0030` (zero) to `U+0039` (nine).

Latin characters are all Unicode code points from `U+0041` (capital `A`) to `U+005A` (capital `Z`) and from `U+0061` (lower `a`) to `U+007A` (lower `z`)
which are all characters from the [Latin alphabet](https://en.wikipedia.org/wiki/Latin_alphabet).

```ebnf
character = ? any Unicode glyph ? ;

white_space_character = ? any white-space character ? ;

none_white_space_character = ? any none white-space character ? ;

any_character = white_space_character | none_white_space_character ;

digit = ? 0-9 ? ;

latin_character = ? a-zA-Z ? ;
```

# Space

A space in Unimarkup is one or more [Unicode spaces](https://util.unicode.org/UnicodeJsps/character.jsp?a=0020) `U+0020`, or Unicode tabs `U+0009`.

**Note:** Multiple spaces or tabs are treated as one Unicode space.

```ebnf
tab = ? Unicode code point U+0009 ? ;

tab_or_space = tab | ? Unicode code point U+0020 ? ; 

space = tab_or_space , { tab_or_space } ;
```

# Line break

Any character sequence that forces a new line, is treated as a line break.
The sequence depends on the used OS.

**Note:** An explicit new line using a backslash `\` at the end of a line is not considered as line break.

```ebnf
line_break = ? any character sequence forcing a new line (OS dependent) ? ;
```

# Line

A line is a sequence of characters except [line break](#line-break) characters.

```ebnf
line = { any_character } - line_break ;
```

# Blank line

A blank line consists of one or more subsequent empty lines.
An empty line is either a line that only consists of white-space characters, or the start and end of a file.

**Note:** Multiple blank lines are treated as one blank line.

```ebnf
empty_line = [ line_break ] , { white_space_character } , [ line_break ] 
             | ? start of file ? | ? end of file ? ;

blank_line = empty_line , { empty_line } ;
```

# Element

A Unimarkup element consists of special character sequences around other characters, that define how the enclosed characters get rendered.

Every element has a unique element type that is used to define the context in which the element may be used.

# Element group

There are Unimarkup elements with similar syntax and/or restrictions that are combined to element groups.
An element group may again have nested element groups.

# Element type

Unimarkup has an implicit type system for Unimarkup elements. Every element and element group has a unique type.

# Type class

A type class identifies where a type of this class is allowed to be used.
Available type classes are listed in the [type system](TypeSystem.md#type-class).

# Content

A content describes any character sequence.

# Rendering

Rendering is the process to convert Unimarkup content into any of the available output formats.

# Root file

The root file is a Unimarkup file that is the single entry point to get a rendered output.

# Document

A document refers to one or more files that are needed to get a rendered output.

# Document flow

A document flows from the highest point of the document, which is the first line of the root file, to the lowest point of the document, which is the last line of the root file.

**Note:** Above refers to content that is closer to the highest point compared to the current one.

**Note:** Below refers to content that is closer to the lowest point compared to the current one.

# Heading height

There are six heading levels ranging from 1 to 6. The heading at level 1 is considered as the highest level and 6 as the lowest.

# Section

A section refers to the content between two headings.

**Note:** The next section refers to section that is at least at the same heading level or higher.

**Note:** Next sections refers to two or more sections that are below the current section.

# Verbatim text

A verbatim text is a sequence of characters that is taken as is without any interpretation of those characters.

# List entry

A list entry is one element of a list element.
