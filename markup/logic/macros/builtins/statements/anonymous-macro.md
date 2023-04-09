# Anonymous macro

This macro is useful to execute arithmetic macros in a more readable form.

The return type depends on the executed statement.

```
{#_ <any macro statement>/}
```

**Example:**

```
Without the anonymous macro: {#+ var1, var2 /}

Using the anonymous macro: {#_ var1 + var2 /}
```
