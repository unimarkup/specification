# Generics

Generics are type placeholders that may be used for [contracts](/markup/logic/contracts/README.md) and [macros](/markup/logic/macros/README.md).

**Note:** `<>` are not used for placeholders in the examples.

```
{#macro myMacro<T>(myVar: T) int}
  macro body
{/end}
```

## Restrict generic types

Generic types may be restricted to only represent a limited number of types,
or enforce that a generic type must comply to specific contracts.

**Type restriction:**

```
{#macro myMacro<T: type1 | type2>(myVar: T) int}
  macro body
{/end}
```

**Contracts:**

```
{#macro myMacro<T: contract1 & contract2>(myVar: T) int}
  macro body
{/end}
```

## Direct type restriction

Instead of defining a generic type, type restrictions and contracts may be set directly as type definition.
This is useful if the generic type would only be used once.

```
{#macro myMacro(myVar: type1 | type2) int}
  macro body
{/end}
```
