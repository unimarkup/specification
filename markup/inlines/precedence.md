# Precedence

The precedence defines what inline elements may be nested inside others.
Elements with the highest precedence may not include any elements of lower precedence. If an element of lower precedence is inside one of higher precedence, it must be considered as plain content.

The following list shows the element precedence with lower number meaning higher precedence.

1. [Comments](/markup/inlines/comments)
2. [Verbatim-formatting](/markup/inlines/formattings#verbatim) and [math-formatting](/markup/inlines/formattings#math)
3. [Boxes](/markup/inlines/boxes/README)
4. All other inline elements
