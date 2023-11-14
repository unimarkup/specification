# Precedence

The precedence defines the order in which keywords may be used to create elements.
Elements with higher precedence may not include any elements of lower precedence.
If an element of lower precedence is inside one of higher precedence, it must be considered as plain content.

The following list shows the element precedence with lower number meaning higher precedence.

1. [Comments](/markup/inlines/comments.md) or [doc comments](/markup/logic/doc-comments.md)
2. [Attributes](/markup/decorators/attributes.md) or [logic](/markup/logic/README.md)
3. [Verbatim block](/markup/blocks/enclosed/verbatim-block.md)
4. All other block elements
5. [Boxes](/markup/inlines/boxes/README.md), [explicit substitutions](/markup/inlines/explicit-substitutions/README.md), [Verbatim-formatting](/markup/inlines/formattings.md#verbatim), and [math-formatting](/markup/inlines/formattings.md#math)
6. [Implicit substitutions](/markup/inlines/implicit-substitutions/README.md)
7. All other inline elements

**Note:** Implicit substitutions are intentionally defined to not conflict with other elements.
