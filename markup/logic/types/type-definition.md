# Type definition

**WIP**

## Struct type definition

```
(
  <field name 1>: <type name> := <optional default value>,
  <field name 2>: <type name>,
)
```

**Note:** Macro parameters have the same syntax.

## List type definition

`List<T>`

### Single dimension

```
type1[]
```

### Two and more dimensions

Every `[]` adds another dimension.

```
2D-Type[][]
```

```
3D-Type[][][]
```

## Generic instantiated type definition

**Note:** `<>` are not used as placeholders in this example.

```
generic-type<concrete-type>
```

Multiple generics:

```
generic-type<concrete-type1, concrete-type2>
```

## Case type definition

```
| type1 | type2 | type3
```

**Note:** The first `|` is optional.

**Example with a match statement:**

```
{#type someBlock := heading | verbatim-block/}
{#var myBlock: someBlock := block(# Heading)/}

{#match myBlock}
  {:case heading}
    {$myBlock}
  {:case verbatim-block}
    **Usage:**

    {$myBlock}
{/end}
```

## Macro type definition

```
(param1: type1, param2: type2) returnType
```
