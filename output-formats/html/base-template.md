# Base template

Every Unimarkup document rendered to HTML must use this template as base.

**Note:** Placeholder values are marked with `{}`.

```html
<!DOCTYPE HTML>
<html lang="{`lang` i18n configuration option}">
  <head>
    <meta http-equiv="Content-Type" content="text/html; charset=UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1" />
    <meta name="author" content="{comma separated values of the `authors` configuration option}" />
    <title>{`title` configuration option}</title>
  </head>
  <body>
  </body>
</html>
```
