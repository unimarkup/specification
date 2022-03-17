# Introduction

Unimarkup has an implicit type system for Unimarkup elements. Every element has a unique type to restrict the usage of elements in certain context.

# Type class

A type class identifies where a type of this class is allowed to be used.

**The following type classes are possible:**

- `General` ... This type may be used for elements, attributes, macros and variables
- `Attribute` ... This type may only be used for attributes and inside the preamble
- Type classes for elements
	- `Group` ... Referring to an element group
	- `Single` ... Referring to a single element

# Generic type

Generic types are marked with `<>` at the end of the type name in the type definition.
To use a generic type, a type must be set between `<>`.

**Example:**

```
list<paragraph>
```

# General types

General types may be used for element, attribute, variable and macro types.

**Available general types:**

: `bool` :
:-- `General`
:
: This type accepts the two values `true` and `false`.
: Both values are case-insensitive, so `True` is the same as `true`.

: `character` :
:-- `General`
:
: This type accepts one character.

: `text` :
:-- `General`
:
: This type accepts zero or more characters.

**Note:** Elements, macros and variables of type `text` output the characters as is without rendering.

**Note:** The `text` type internally is of type `list<character>`.

: `word` :
:-- `General`
:
: This type accepts a sequence of none-white-space characters.

**Note:** The `word` type internally is of type `list<character>`.

: `number` :
:-- `General`
:
: This type accepts [JSON numbers](https://restfulapi.net/json-data-types/).

: `integer` :
:-- `General`
:
: This type accepts integer numbers.

: `natural` :
:-- `General`
:
: This type accepts natural numbers starting at zero.

: `positive` :
:-- `General`
:
: This type accepts natural numbers starting at one.

: `negative` :
:-- `General`
:
: This type accepts negative integer numbers.

: `list<>` :
:-- `General`
:
: This generic type accepts a list of the type given between `<>`.

: `range[<from>:<to>]` :
:-- `General`
:
: This type accepts a range of integer values starting from the integer value set instead of `<from>`
: up to the included integer value set instead of `<to>`. The value of `to` must be at least as high as `from`.
:
: Spaces are allowed to separate the integer values.

**Example:**

```
range[20 : 30]
```

**Note:** The range type is internally treated as `list<integer>`.

: `enum` :
:-- `General`
:
: This type only accepts certain values.
: Allowed values must be set in the type description.

**Example:**

```
: `some_enum` :
:-- `enum`
:
: This type only allows:
:
: - `value1` ... some description
: - `value2` ... some description
```
