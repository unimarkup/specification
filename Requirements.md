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

There are some Unimarkup types that may be used for element, attribute, variable and macro types.
Those types must be defined in the [general types](TypeSystem.md#general-types) section using [definition blocks](Frontend_Reference.md#definition-block).
`General` must be set in the classifier.

**Format for a general type definition:**

~~~
: `<type name>` :
:-- `General`
:
: <general type description>
~~~

## EBNF overview

EBNF defines rules that describe how a sequence of characters must look like, to fulfill those rules. EBNF may be used to express definitions in a more formal way.

The following symbols are used with EBNF:

- `=` ... Defines a new rule with the name of the rule to the right
- `,` ... Concatenates two rules or terminal strings
- `;` ... Defines the end of a rule definition
- `|` ... Separation between rules or terminal strings where either side fulfills the rule
- `[ ]` ... Rules or terminal strings between the brackets are optional to fulfill the rule
- `{ }` ... Rules or terminal strings between the curly braces are optional and may repeat to fulfill the rule
- `( )` ... Group parts of a rule together
- `" "` or `' '` ... Terminal string, where every character between is treated as is
- `(* *)` ... Comments may be added between
- `? ?` ... Allows to describe the content of character sequences
- `-` ... An exception, that is fulfilled, if the left side is fulfilled, and the right side is not

**Note:** This is a simplification to get the basic idea.

# Frontend requirements
## Attribute definition

Attributes that are specific to an element must be defined in [definition blocks](Frontend_Reference.md#definition-block) in the element attribute definition.
If an attribute needs a type that is not defined in any type group and not needed by any other attribute, element, macro or variable, the restrictions of the attribute may be described directly
in the attribute description without creating a new attribute type.
Otherwise, the type should be defined in one of the attribute type groups. The definition format of an attribute type is defined under [attribute type definition](#attribute-type-definition).
Nested attributes must be defined in nested definition blocks. 

**Format for an attribute definition:**

~~~
: `"<attribute name>"` :
:-- `<attribute type>`
:
: <attribute description>

: `"<attribute name>"` :
:-- Attribute uses some special restrictions
:-- not covered by any other type.
:
: <attribute description>
~~~

## Attribute type definition

Attribute types must be defined in [definition blocks](Frontend_Reference.md#definition-block) and `Attribute` must be set in the classifier.

**Format for an attribute type definition:**

~~~
: `<attribute type name>` :
:-- `Attribute`
:
: <attribute type description>
~~~

## Element definition

The element definition must describe the syntax and usage of an element in English.
For a more precise definition, especially for complex elements, the [Extended Backus Naur Form](https://en.wikipedia.org/wiki/Extended_Backus%E2%80%93Naur_form) should be used additionally.
If EBNF is used, it should be placed inside one verbatim block. Syntax highlighting may be set for the verbatim block by setting `~~~ebnf` as block starting.

### Element usage definition

Every element definition must have at least one usage example where the usage of the element is seen.
All examples are enclosed in verbatim blocks with `**Usage:**` set before the first verbatim block.

If any other definition is between two usage verbatim blocks, `**Usage:**` must be set per verbatim block.

**Example:**

~~~~
**Usage:**

~~~
<one or more examples showing the usage of an element>
~~~
~~~~

### Element type definition

Every element must at least define one type for the element. Each type is defined using one [definition block](Frontend_Reference.md#definition-block). `**Type:**` must be set before the first definition block.
If more than one type is defined, `**Types:**` must be used instead.

Element types of type class `Single` must be defined in nested definition blocks of the associated type of type class `Group`, if the group type is defined inside the same element definition.

**Note:** Available element type classes are defined in the [type class](Terminology.md#type-class) section.

**Format for an element type definition:**

~~~
: `<type name>` :
:-- `<element type class>`
:
: <type description>
~~~

**Example:**

~~~
**Types:**

: `my_type` :
:-- `Group`
:
: my_type description.
:
: : `sub_type` :
: :-- `Single`
: :
: : sub_type description.
~~~

### Element attribute definition

Every element definition must list the supported attributes below `**Attributes:**`. If only one attribute is defined, `**Attribute:**` must be used and if an element has no attributes, `**No attributes**` must be used instead.
General or element group attributes that are supported, are referenced in a bullet list before the element specific ones. The definition format for attributes is defined under [attribute definition](#attribute-definition).

**Example:**

~~~
**Attributes:**

- [Block attributes](#block-attributes)

: `"specific-attribute"` :
:-- `paragraph`
:
: Description of this specific attribute.
:
: : `"sub-attribute"` :
: :-- `number`
: :
: : Description of the sub-attribute.
~~~

### Element preamble options definition

Every element definition must list the supported preamble options below `**Preamble options:**`. For only one preamble option, `**Preamble option:**` must be used.
If there are no options available, `**No preamble options**` must be written.
Available preamble options must be set in definition blocks in the same format as defined under [attribute definition](#attribute-definition).

### Element definition layout

The general layout for all element definitions should follow the structure below.

~~~~
# <element name>

<element definition>

~~~ebnf
<optional EBNF>
~~~

<optional content>

**Usage:**

~~~
<element usage>
~~~

<optional content>

**Type:**

<element type>

**Attributes:**

<element attributes>

**Preamble options:**

<element preamble options>
~~~~

**Note:** In the layout above, `<optional content>` may contain any Unimarkup content, but should be restricted to short paragraphs and notes.


