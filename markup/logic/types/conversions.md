# Conversions
## Explicit type conversion

```
<typename>(<memorable or value to be converted>)
```

## Implicit type conversion

To get implicit type conversions from type `X` to type `Y`,
the generic `from<A, B>` macro must be implemented with `X = A` and `Y = B`.

Values of type `A` may be accessed using constant `self`.

```
{#from int to real}
  {#_ self * 1.0/}
{/end}
```

If the `from<A, B>` macro is implemented, all memorables of type `A` may be used where type `B` is required without explicit conversion.
Furthermore, all macros with first parameter of type `B` may be accessed via dot notation for memorables of type `A`.
If `B` has memorables or types as fields, these may also be accessed using dot notation for memorables of type `A`.

**Note:** If `A` and `B` have fields of the same name, but different type, dot notation always refers to the field of the original type.

**Note:** Explicit type conversion may still be used between types implementing `from<A, B>`.
