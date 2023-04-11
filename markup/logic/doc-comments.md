# Doc comments

Doc comments may be used to provide a description for a logic element.
Every line starting with `;;;` directly before a logic element is created, is considered as doc comment.
It is also possible to set doc comments in struct definitions before every field.

**Type:** `doc-comment`

## Mentioning parameters in doc comments

Macro parameters may be mentioned in doc comments by referring to them using `{$<parameter name>}`.

As convention, parameters should be described using the [description list](/markup/blocks/indents/lists/description-list) syntax.

Parameter names must be used in the rendered doc comment without `{$ }`.

**Example:**

```
;;; myMacro does something.
;;;
;;; - {$param1} ... the first parameter
;;; - {$param2} ... the second parameter
{#macro myMacro(param1: int, param2: int) int/}
```

**Note:** An implementation should include the type and default value of a parameter in the description list.

## Macro return in doc comments

The return type may be referred to using either `return` or `returns`, using the same syntax as mentioning parameters.
Both variants are case-insensitive.

The variant must be used in the rendered doc comment as is without `{$ }`.

**Example:**

```
;;; myMacro does something.
;;;
;;; - {$returns} ... some value
{#macro myMacro(param1: int, param2: int) int/}
```

**Note:** An implementation should include the return type in the description list.
