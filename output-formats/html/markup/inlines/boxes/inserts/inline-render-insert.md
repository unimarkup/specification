# Inline render insert

Since supported renderer may vary between implementations,
the conversion examples are defined for Unimarkup file inserts.
The rendered output of other inserted content may vary between implementations.

**Note:** The following example assumes the content ``**content** of `someFile.um` that is *rendered*`` inside the file `someFile.um`.

```
[''Some file description](someFile.um)
```

renders to

```html
<strong>content</strong> of <pre>someFile.um</pre> that is <em>rendered</em>
```
