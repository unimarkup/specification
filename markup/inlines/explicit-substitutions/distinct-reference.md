# Distinct reference

**WIP**

A distinct reference may be used to explicitly state the property of a literature reference that is to be inserted.
For this, the literature ID, followed by an optional property set after `.`, must be surrounded by `&&`.

**Note:** If no property is set, `authors` must be chosen as fallback.

**Note:** The same ID constraints apply as defined for [literature referencing](/markup/inlines/boxes/referencing/literature-reference).

**Usage:**

```
&&Gruber2004&& invented &&Gruber2004.title&& in &&Gruber2004.year&&.
```

The above is converted into:

```
John Gruber invented Markdown in 2004.
```

**Note:** The ID *Gruber2004* must be set accordingly in the given references for the above example to work.
