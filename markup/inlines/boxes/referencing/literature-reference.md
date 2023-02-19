# Literature referencing

**WIP**

Literature references are used to reference books, articles, journals or websites and use the [Citation Style Language](https://citationstyles.org/) to render literature depending on the provided CSL file.
To reference a literature, the literature meta-data and CSL file must be provided using one of the [configuration options](/configuration/README).
The literature meta-data must be in a format that is supported by the used CSL processing tool. See the documentation of the used Unimarkup implementation for more information.

A literature is referenced using the ID (called *label* in BibTeX) of a literature entry in the form `[&&<literature-id>]`.
It is possible to reference more than one literature with `[&&<first-literature-id>, <second-literature-id>]`.

Depending on the used CSL, citations are either `in-text` or `note`. More information may be found in the [CSL specification](https://docs.citationstyles.org/en/1.0.1/specification.html).
In the `note` variant, literature references must not be rendered at the inline position of the literature reference. The rendered position must be as defined in the [note references](/markup/inlines/boxes/referencing/note-reference) section, but must not be combined with regular note references.

**Note:** If a literature ID has more than one definition, the behavior depends on the used CSL processor tool.

**Note:** Literature ID restrictions depend on the used CSL processor tool, but must not include `&`, `.`, `:`, `,` and `]`.

**Usage:**

```
This text has some literature reference [&&literature-id]
This text has more than one literature reference [&&id-1, id-2].
```

**Type:** `literature-referencing`
