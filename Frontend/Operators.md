# Operators

Operators are similar to macros, and provide functionalities that are common to most programming languages.
They are prefixed with `#` instead of `@`. A whitespace after the operator name is mandatory.
The usage restriction depends on the return type of an operator.

It is not possible to define own operators.

## Operator usage

The usage is similar to macros, but the parameter position is fixed, therefore,
not requiring parameters to be named, nor enclosing them in parentheses.

```
{#+ {2},{3}}

{#if {%booleanVar}, {text returned on `true`}, {text returned on `false`}}

{#if {%booleanVar}, {some text}, {#if {%otherVar}, {text returned on `false, true`}}}
```

## Available operators

The available operators in Unimarkup are given in the format:

```
{#<operatorname with optional generic> {<parameter 1>}, {<parameter 2>}, ..., {<parameter n>} -> <return type>}
```

Available operators in Unimarkup:

- `{#:=<T> {assignee:T}, {assignor:T} -> None}` ... Value of set *assignor* is assigned to set *assignee*
- `{#+<T(number)> {a:T}, {b:T} -> T}` ... Values `a` and `b` are added, and the result is returned
- `{#-<T(number)> {a:T}, {b:T} -> T}` ... Value `b` is subtracted from `a`, and the result is returned
- `{#/<T(number)> {a:T}, {b:T} -> T}` ... Value `a` is divided by `b`, and the result is returned
- `{#*<T(number)> {a:T}, {b:T} -> T}` ... Values `a` and `b` are multiplied, and the result is returned
- `{#%<T(number)> {a:T}, {b:T} -> T}` ... Returns the result of `a mod b`
- `{#+<T(number)> {a:T}, {b:T} -> T}` ... Values `a` and `b` are added and the result is returned
- `{#if<T> {condition:boolean}, {consequent:T}, {alternative:T} -> T}` ... Conditional operator that takes the `consequent` if the `condition` evaluates to `true`. Otherwise, the `alternative` is taken.
- `{#for<T> {list:list}, {body:T} -> list<T>}` ... Iterates `body` over all elements of `list` returning a list containing the resulting `body` of each iteration. The variable `{%item}` may be used in the `body` to access the list item of the current iteration (Type of `{%item}` depends on the given list).

;;mhatzl add more operators
