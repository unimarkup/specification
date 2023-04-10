# Style guide
## Placeholder text

Any content that is between `<>` is used as placeholder value to provide context.
The `<>` keywords are also part of the placeholder value.

If an element breaks this convention, it must be stated explicitly. 

## Notes

A note is used to highlight information concerning usage restrictions, to prevent wrong usage, or about the rendering behavior of an element.

**Note:** For now, notes are set by starting a new line with `**Note:**` followed by one space and surrounded by blank lines.\

## List ending

No punctuation must be set if a list entry consists only of one sentence. Otherwise, a punctuation must be set at the end of this list entry.

## Naming conventions

For better consistency and readability, the following naming conventions are used in this specification.

### Macro naming

Macro names should be verbs and must be written in [**camelCase**](https://en.wikipedia.org/wiki/Camel_case).

**Example:**

```
{#renderSomething}
```

### Variable and readonly naming

Variable and readonly names must be written in [**camelCase**](https://en.wikipedia.org/wiki/Camel_case).

**Example:**

```
{%someVariable}
```

### Constant naming

Constant names must be written in [SCREAMING_SNAKE_CASE](https://en.wikipedia.org/wiki/SCREAMING_SNAKE_CASE).

**Example:**

```
{%CONSTANT_VARIABLE}
```
