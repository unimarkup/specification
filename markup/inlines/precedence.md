# Precedence

The precedence defines what inline elements may be nested inside others.
Elements with the highest precedence may not include any elements of lower precedence. If an element of lower precedence is inside one of higher precedence, it must be considered as plain content.

The following list shows the element precedence with lower number meaning higher precedence.

1. [Comments](/markup/inlines/comments) or [doc comments](/markup/logic/doc-comments)
2. [Anonymous macro](/markup/logic/macros/builtins/statements/anonymous-macro)
3. [Verbatim-formatting](/markup/inlines/formattings#verbatim) and [math-formatting](/markup/inlines/formattings#math)
4. [Implicit substitutions](/markup/inlines/implicit-substitutions/README) and [explicit substitutions](/markup/inlines/explicit-substitutions/README)
5. [Boxes](/markup/inlines/boxes/README)
6. All other inline elements
