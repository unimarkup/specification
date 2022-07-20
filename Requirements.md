# General requirements

The focus of Unimarkup is

- Usability
- Consistency
- Internationalization
- Flexibility

## Indicating requirement levels

The keywords **must**, **must not**, **should**, **should not**, **may** and **optional** are used as described in [rfc2119](https://datatracker.ietf.org/doc/html/rfc2119).

## Stick to Unimarkup

The specification itself must be written in Unimarkup.

## General type definition

General types must be defined in the [general types](TypeSystem.md#general-types) section using [definition blocks](Frontend_Reference.md#definition-block).
`General` must be set in the classifier.

**Format for a general type definition:**

```
: `<type name>` :
:-- `General`
:
: <general type description>
```

# Frontend requirements
## Attribute definition

Attributes that are specific to an element must be defined in [definition blocks](Frontend/AtomicBlocks.md#definition-block) in the elements attribute definition.
If an attribute needs a type that is not defined in any type group and not needed by any other attribute, element, macro or variable, the restrictions of the attribute may be described directly
in the attribute description without creating a new attribute type.
Otherwise, the type should be defined in one of the attribute type groups. The definition format of an attribute type is defined under [attribute type definition](#attribute-type-definition).
Nested attributes must be defined in nested definition blocks. 

**Format for an attribute definition:**

```
: `"<attribute name>"` :
:-- `<attribute type>`
:
: <attribute description>

: `"<attribute name>"` :
:-- Attribute uses some special restrictions
:-- not covered by any other type.
:
: <attribute description>
```

## Attribute type definition

Attribute types must be defined in [definition blocks](Frontend/AtomicBlocks.md#definition-block) and `Attribute` must be set in the classifier.

**Format for an attribute type definition:**

```
: `<attribute type name>` :
:-- `Attribute`
:
: <attribute type description>
```

## Element definition

The element definition must describe the syntax and usage of an element in English.

### Element usage definition

Every element definition must have at least one usage example where the usage of the element is seen.
All examples are enclosed in verbatim blocks with `**Usage:**` set before the first verbatim block.

If any other definition is between two usage verbatim blocks, `**Usage:**` must be set per verbatim block.

**Example:**

````
**Usage:**

```
<one or more examples showing the usage of an element>
```
````

### Element type definition

Every element must at least define one type for the element. Each type is defined using one [definition block](Frontend/AtomicBlocks.md#definition-block).
`**Type:**` must be set before the first definition block.
If more than one type is defined, `**Types:**` must be used instead.

Element types of type class `Element` must be defined in nested definition blocks of the associated type of type class `Group` if the group type is defined inside the same element definition.

**Note:** Available type classes are defined in the [type class](Terminology.md#type-class) section.

**Format for an element type definition:**

```
: `<type name>` :
:-- `<element type class>`
:
: <type description>
```

**Example:**

```
**Types:**

: `my_type` :
:-- `Group`
:
: my_type description.
:
: : `sub_type` :
: :-- `Element`
: :
: : sub_type description.
```

### Element attribute definition

Every element definition must list the supported attributes below `**Attributes:**`. If only one attribute is defined, `**Attribute:**` must be used.
If an element has no attributes, this definition section may be skipped.
General or element group attributes that are supported, must be referenced in a bullet list before the element specific ones. The definition format for attributes is defined under [attribute definition](#attribute-definition).

**Example:**

```
**Attributes:**

- [Block attributes](#block-attributes)

: `"specific-attribute"` :
:-- `Paragraph`
:
: Description of this specific attribute.
:
: : `"sub-attribute"` :
: :-- `Number`
: :
: : Description of the sub-attribute.
```

### Element definition layout

The general layout for all element definitions should follow the structure below.

````
# <element name>

<element definition>

**Usage:**

```
<element usage>
```

**Type:**

<element type>

**Attributes:**

<element attributes>
````
