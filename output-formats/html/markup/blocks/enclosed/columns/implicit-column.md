# Implicit column block

**WIP**

```
|||2| 
This content may have any form of unimarkup content. It is automatically distributed over two columns.

# Header

Some *more* text.
|||#|
```

renders to

```html
<div style="column-count: 2">
  <p>This content may have any form of unimarkup content. It is automatically distributed over two columns.</p>
  <h1>Header</h1>
  <p>Some <em>more</em> text.</p>
</div>
```
