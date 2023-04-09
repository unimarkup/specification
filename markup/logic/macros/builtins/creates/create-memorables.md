# Create memorables

**WIP**

## Create variables

```
{#var <variable name>:<variable type> := <optional default value>/}
```

## Create constants

```
{#const <constant name>:<constant type> := <constant value>/}
```

## Create read only variables

```
{#readonly <readonly name> := <variable name>/}
```

Alternative:

```
{#ro <readonly name> := <variable name>/}
```

**Note:** The variable a *readonly* refers to should be private. Otherwise, a user could simply use the public variable instead.
