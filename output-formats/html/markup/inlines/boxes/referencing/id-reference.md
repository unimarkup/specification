# ID referencing

```
[Some text]{ id: "some-id" }

Referencing [##some-id: some text box].
```

renders to

```html
<p id="some-id">Some text</p>

<p>Referencing <a href="#some-id">some text box</a>.
```
