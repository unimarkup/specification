# Parameters

Parameters of macros are similar to constants, but do not require default values.
If a default value is set, the parameter becomes optional, and the macro may be called without setting a new value for this parameter.

Any parameter is accessible inside the macro body like a readonly memorable.

## Named and positional arguments

When calling a macro, parameters may be given in two ways:

- **Named**

  ```
  {#myMacro param1 := <memorable or value>, param2 := <memorable or value>/}
  ```

- **Positional**

  **Note:** Positional parameters must be set before any named parameter is set if both variants are mixed.

  ```
  {#myMacro <memorable or value>, <memorable or value>/}
  ```

## Inner macros

If a return value of a macro should be used as parameter, the inner macro must be called using `innerMacro(<parameters>)`.

```
{#myMacro myMacro(1, 2), 3/}
```
