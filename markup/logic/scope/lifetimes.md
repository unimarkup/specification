# Lifetimes

Every memorable has a certain lifetime.
This lifetime defines how long the data of a memorable may be accessed.

A lifetime is closely related to the [visibility](/markup/logic/scope/visibility) of a memorable. If a memorable is not visible anymore, its lifetime also ends.

If a lifetime ends, an implementation is free to drop the associated data, but may keep it if the underlying data was passed to another memorable that is still visible.
Data is passed from one memorable to another by [assignment](/markup/logic/macros/builtins/statements/assignment).

**Example:**

```
{#const docLifetime := 1/}

{#macro myMacro(macroLifetime: int) int}
  {#var innerMacroLifetime := 2/}

  {#_ innerMacroLifetime + macroLifetime + docLifetime/}
{/end}

{#myMacro(docLifetime)/}
```
