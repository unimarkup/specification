# Markup

This section defines the conversion from Unimarkup elements to HTML output.

Explicitly set `id` and `class` attributes for an element must be set in the rendered output. If they are not set explicitly, the implementation may set automatically generated ones, or not set these attributes at all. 

**Note:** Only explicitly set `id` and `class` attributes are set on HTML output examples. However, an implementation is free to set automatically generated values.   

**Examples are given in the following format:**

````
```
<Unimarkup content>
```

renders to

```html
<HTML content>
```
````
