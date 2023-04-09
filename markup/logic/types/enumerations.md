# Enumerations

**WIP**

Enumerations are a special kind of [case type definitions](/markup/logic/types/type-definition#case-type-definition).
Every type of an enumeration is unique, and would require to be wrapped in `type()`.
The `enum` macro reduces the need for this wrapper.

**Example:**

```
{#type enum1 := type(one) | type(two) | type(three)/}
```

becomes

```
{#enum enum1 := one | two | three/}
```
