# Text block
## With attributes

```
[[[
Any Unimarkup text **may** be
inside a text block
]]]{ id: "my-block" }
```

renders to

```html
<div id="my-block">
     <p>Any Unimarkup text <strong>may</strong> be inside a text block</p>
</div>
```

## Without attributes

```
[[[
Any Unimarkup text **may** be
inside a text block
]]]
```

renders to

```html
<div>
     <p>Any Unimarkup text **may** be inside a text block</p>
</div>
```
