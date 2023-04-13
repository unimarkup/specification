# Unimarkup

Unimarkup as output may be used to strip the given content from unnecessary whitespace.
Multiple contiguous blank lines are converted to one, and contiguous none line-breaking whitespace is converted to one space.

Besides optimizing whitespace, all implementations must convert implementation specific markup,
like field boxes/blocks, macros, and memorables,
to elements supported by the basic Unimarkup specification.
This offers better interoperability between implementations.

**Note:** Output from renderer, highlighter and math-markup may not be converted to basic elements.
This creates some difference between implementations, but keeps the content more readable.
