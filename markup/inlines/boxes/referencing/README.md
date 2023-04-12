# Referencing

**WIP**

There are several reference variations in Unimarkup.

The syntax builds on the general [inline box](/markup/inlines/boxes/README.md) syntax.
Every referencing variation has its own keyword followed by an ID, that is set immediately after `[`.

An optional display text may be given after the ID, by setting `:`.
This allows to overwrite the default text for this ID.

**Note:** If there is no default text for a reference variation, the first explicitly set text must be used as default text for all further references.

**Example:**

```
A paragraph that references [##some-image-id: Custom referencing text].
```

**Type:** All referencing elements are part of the `referencing` type.

**Variations:**

- [ID referencing](/markup/inlines/boxes/referencing/id-reference.md)
- [Literature referencing](/markup/inlines/boxes/referencing/literature-reference.md)
- [Note referencing](/markup/inlines/boxes/referencing/note-reference.md)
