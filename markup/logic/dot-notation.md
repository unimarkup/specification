# Dot notation

**WIP**

## Macros

If the first parameter-type of a macro is equal to the type of a memorable, or the type itself is set, the macro may be called via dot notation that consumes the first parameter.

```
{#macro myMacro(param1: int) int}
  {#_ param1 * param1/}
{/end}

{#const myConst: int := 1/}

{#_ myConst.myMacro()/}
```

## Struct fields

The fields of a struct may be accessed via dot notation.
If a field is again a struct, those fields may again be accessed via dot notation.

```
{#const someStruct := (
  field1: int := 1,
  field2: (
    nestedField: int := 2,
  ),
)}

{#_ someStruct.field1 + someStruct.field2.nestedField/}
```

## Contracts

Contracts have the same syntax as structs, so the dot notation is the same as for structs.
