# Variables

It is possible to use variables in Unimarkup either global per Unimarkup document,
or inside macros. A variable may be of any supported Unimarkup type.

A variable is uniquely identified by a namespace and the variable name.
Every variable is inside the namespace of the Unimarkup file in which it is defined.

## Variable definition

A variable may be defined using the following syntax:

```
{%<variable name>: <type> {<optional initial value>}}

{%myVar: text {Some initial text}}
```

A global variable definition is not allowed inside a nested block and may only be surrounded by blank lines or other global variable definitions.

Variable definitions inside macros must be separated by blank lines from other Unimarkup elements, and must only be accessed inside a macro scope after they are defined.
Variables defined inside macros are called *local variables* and are bound to the scope of the macro. 

## Variable usage
### Global variable usage

Global variables may be accessed anywhere in a Unimarkup document depending on the variable type.

```
{%author: text {Manuel Hatzl}}

Some paragraph written by {%author}.
```

### Local variable usage

Local variables are defined inside a macro and are bound by the scope of the macro.
It is not possible to access them before they are defined.

```
{@myMacro(a:positive, b:positive) positive =>
  {%localVar: positive}

  {#:=({%localVar}, {#+({%a}, {%b})})}
  
  {#return({%localVar})}
}
```

## Namespace and variable names

The same rules apply as defined for [macros](Macros.md/#namespaces-and-macro-names).

## Predefined variables

The following global variables are predefined, and may be used inside a Unimarkup document.

;;mhatzl
