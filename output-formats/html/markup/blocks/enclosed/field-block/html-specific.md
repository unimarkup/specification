# HTML specific

The following field blocks are supported for the HTML output.

## `html`

May include HTML elements that are allowed inside the HTML `body`, except `script` and `style`.

```
[[[<html>
  <h1>Heading</h1>
]]]
```

renders to

```html
<h1>Heading</h1>
```

## `article`

Defines an article region.

```
[[[<article>
  # Article heading

  Some content.
]]]
```

renders to

```html
<article>
<h1>Article heading</h1>
<p>Some content.</p>
</article>
```

## `aside`

Defines content to display aside other content.

```
[[[<aside>
  # Aside heading

  Some content.
]]]
```

renders to

```html
<aside>
<h1>Aside heading</h1>
<p>Some content.</p>
</aside>
```

**Note:** Headings inside an `aside` block must not be part of the table of content.
