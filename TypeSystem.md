# Introduction

Unimarkup has an implicit type system for Unimarkup elements, but an explicit type system
for macros, variables and operators. Every element has a unique type to restrict the usage of elements in certain contexts.
Besides element types, there are also some general types that may be used for attributes, macros, variables and operators.
In addition, group types provide the possibility to types in a hierarchical manner.
This helps with generalisation of macro and variable parameters.

# Type class

A type is assigned to one of the following classes:

- `Element` ... Type of a Unimarkup element
- `General` ... Non-element type that may be used for attributes, macros, variables and operators 
- `Group` ... Type that groups several types of `Element` or `General` class

**Note:** A group must only group types of the same class, or another group type with types of the same class.

# General types

The following types are of class `General`:

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
:
: **Note:** The `text` type internally should be of type `list<character>`.

: `word` :
:-- `General`
:
: This type accepts a sequence of none-white-space characters.
:
: **Note:** The `word` type internally should be of type `list<character>`.

: `number` :
:-- `Group`
:
: This type accepts [JSON numbers](https://restfulapi.net/json-data-types/).
:
: : `integer` :
: :-- `General`
: :
: : This type accepts integer numbers.
: 
: : `natural` :
: :-- `General`
: :
: : This type accepts natural numbers starting at zero.
: 
: : `positive` :
: :-- `General`
: :
: : This type accepts natural numbers starting at one.
: 
: : `negative` :
: :-- `General`
: :
: : This type accepts negative integer numbers.

: `list<>` :
:-- `General`
:
: This generic type defines a list of the type given between `<>`.

: `range[<from> .. <to>]` :
:-- `General`
:
: This type defines a range of integer values starting from the integer value set for `<from>`
: up to the included integer value set for `<to>`.
: Spaces are allowed to separate the integer values.
:
: **Note:** The value of `to` must be at least as high as `from`.
:
: **Note:** The range type internally should be of type `list<integer>`.
:
: **Example:**
: 
: ```
: range[20 .. 30]
: ```

: `enum` :
:-- `General`
:
: This type only accepts certain values.
: Allowed values must be defined in the type description.
: 
: **Example:**
: 
: ```
: : `some_enum` :
: :-- `enum`
: :
: : This type only allows to set values to:
: :
: : - `uni` ... some description
: : - `markup` ... some description
: ```
