# Precedence

The precedence defines what inline elements may be nested inside others.
Elements with the highest precedence may not include any elements of lower precedence. If an element of lower precedence is inside one of higher precedence, it must be considered as plain content.

The following list shows the element precedence with lower number meaning higher precedence.

1. [Comments](/markup/inlines/comments.md) or [doc comments](/markup/logic/doc-comments.md)
2. [Anonymous macro](/markup/logic/macros/builtins/statements/anonymous-macro.md)
3. [Verbatim-formatting](/markup/inlines/formattings.md#verbatim) and [math-formatting](/markup/inlines/formattings.md#math)
4. [Implicit substitutions](/markup/inlines/implicit-substitutions/README.md) and [explicit substitutions](/markup/inlines/explicit-substitutions/README.md)
5. [Boxes](/markup/inlines/boxes/README.md)
6. All other inline elements
