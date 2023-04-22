# Macros

Macros may be used to help with content reuse.
Unimarkup does not have a runtime, and therefore, all macros are constant expressions.

**WIP**

**Usage:**

```
{#<macroname> <parameter1>, <parameter2>}
  <returned content>
{/end}

{#topLevelSections/}

;;; Returns a bullet list of the top level sections of a document
{#macro topLevelSections() bullet-list}
  {#for section in doc.sections[1]}
    - [##{$section.id}: {$section.title}]
  {/end}
{/end}

;;; Macro to calculate the fibonacci sequence for a given number
{#macro fib(n:int := 0) int}
  {#if n <= 2}
    1
  {:else}
    ;; anonymous macro to execute statements directly
    {#_ fib(n - 1) + fib(n - 2)/}
  {/end}
{/end}

The fibonacci number for 8 = {#fib 8/}
```
