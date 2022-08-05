# Macros

Macros may be used to reduce text duplication, improve consistency across documents, or to provide functionality for out of flow elements.
Macros are similar to functions in most common programming languages.

A macro is uniquely identified by a namespace and the macro name. Every macro is inside the namespace of the Unimarkup file in which it is defined.

## Macro definition

A macro may be defined using the following syntax:

```
;;; Description for this macro
;;; optional multiple description lines
{@macroname<optional generics>(param1:parameter type, param2 : parameter type) return type =>
  macro body
  first line in body defines number of leading spaces that are not part of the body content.
}
```

**Note:** `<>` are mandatory and no placeholders.

Parameters may be accessed in the body like Unimarkup variables.
If no parameter is set, empty parentheses must be used like `{@macroname()}`.

A macro definition is not allowed inside a nested block and may only be surrounded by blank lines or other macro definitions.

### Parameter and return types

A macro parameter type may consist of one or more types allowed in Unimarkup, or using one of the defined generics defined for the macro.
Multiple types must be enclosed in parentheses and separated by `|`.
It is not allowed to use a generic for parameters with multiple types.

The return type is restricted to a single type or generic. If the return type is generic, the generic must
be used as one of the parameter types.

**Usage:**

```
{@myMacro(param1:text, param2:(paragraph|table)) paragraph =>
  body
}

{@myGenericMacro<T>(param1:T) T =>
  {%param1}
}
```

### Generics

Generics may be defined after the macroname. Multiple generics must be separated by `,`.
To restrict the types a generic may have, enclose allowed types in parentheses after the generic.
Allowed types must be separated by `|`.

The name of a generic must not conflict with any allowed Unimarkup type, and only consist of alphanumeric characters.

**Usage:**

```
{@myRestrictedMacro<T(paragraph|table)>(param1:T) T =>
  {%param1}
}
```

### Default parameter values

It is possible to set default values for parameters, making those parameters optional.
The default value may be set after the parameter type, and must be enclosed in curly braces.
If no default value is set, the parameter is mandatory when using the macro.

**Usage:**

```
{@myDefaultMacro(param1:paragraph, param2:paragraph {some default text}) paragraph =>
  {%param1}: {%param2}
}
```

### Macro usage

Parameters defined may be set in any order when using the macro.
The parameter name must be given and the value to be assigned to the parameter enclosed in curly braces.
Multiple parameters are separated by `,`.

`parameter name{content assigned to the parameter}`

**Note:** If a type violation is found, rendering should fail with an error indicating the type violation.

- Defining macros:

  ```
  {@myMacro(a: paragraph) paragraph =>
    Some text: {%a} (as one paragraph).
  }

  {@myMultiMacro(a: paragraph, b: paragraph) paragraph =>
    Some text: {%a} and {%b} (as one paragraph).
  }
  ```

- Using macros:

  ```
  {@myMacro(a{using a parameter})}

  {@myMultiMacro(b{b parameter}, a{using a parameter})}
  ```

## Namespaces and macro names

Namespaces may be used to group macros, since `<namespace>.<macro name>` must be unique across the entire document.
Every Unimarkup file has its own namespace, but it is possible to add namespaces inside a file.

A macro name may consist of any character except `{}@.()%<>` and spaces.
If a `.` is part of the name, the text before `.` is considered as a namespace.

Macros defined in the current Unimarkup file may be accessed without a namespace or starting the macro name with `.`.

## Predefined macros

The following macros are predefined and must be part of every Unimarkup implementation.
Predefined macros must have `um` as namespace.

- `{@<text> um.space()}`: This macro adds one non-breaking space
- `{@<text> um.tab()}`: This macro adds two non-breaking spaces






;; mhatzl

- `{@<inline> um.repeat(%<positive> count %<inline> text}}`: This macro repeats a given text for `count` times
- `{@um.defineHeader{all text}}`: This macro defines a header that is applied to a page. It may be overwritten at any point, only the last macro call is taken for the header
- `{@um.defineFooter{all text}}`: This macro defines a footer that is applied to a page. It may be overwritten at any point, only the last macro call is taken for the footer
- `{@um.defineToc}`: This macro inserts the table of contents at this position
- `{@um.defineRefs}`: This macro inserts references used in the document at this position
- `{@um.defineAbbr}`: This macro inserts abbreviations used in the document at this position
