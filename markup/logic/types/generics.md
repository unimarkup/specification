# Generics

Generics are type placeholders that may be used for [structs](/markup/logic/types/type-definition.md#struct-type-definition) and [macros](/markup/logic/macros/README.md).

**Note:** `<>` are not used for placeholders in the examples.

```
{#macro myMacro<T>(myVar: T) int}
  macro body
{/end}
```

## Restrict generic types

Generic types may be restricted to only represent a limited number of types (disjunction),
or a combination of types (conjunction).

**Type restriction:**

- Disjunction

  ```
  {#macro myMacro<T: type1 | type2>(myVar: T) int}
    macro body
  {/end}
  ```

- Conjunction

  **Note:** Set types must not have fields of same name. 

  ```
  {#macro myMacro<T: type1 & type2>(myVar: T) int}
    macro body
  {/end}
  ```

## Direct type restriction

Instead of defining a generic type, type restrictions may be set directly as type definition.
This is useful if the generic type would only be used once.

```
{#macro myMacro(myVar: type1 | type2) int}
  macro body
{/end}
```
