# Attributes

Attributes may be set on any element that allows them, by wrapping attributes in `{}`.
The attribute position depends on the element, and must be defined per element.

Attributes must be set using CSS syntax: `<property name>: <value>;`.
Nesting attributes must follow the proposed [CSS nesting syntax](https://www.w3.org/TR/css-nesting-1/) using `&` as identifier prefix.

**Note:** The allowed attributes per element depend on the output format.

**Example:**

```
some paragraph { color: red }

[!!some image](/myImg.png){ width: 400px }
```

**Default attributes that must be allowed in all output formats:**

- `id` ... sets the ID of an element (see the [element IDs](/markup/element-ids.md) section for more details)
- `class` ... sets one or more classes to an element (multiple classes must be separated by spaces)
