# Abbreviation

There are two variants:

- **First abbreviation occurrence in document flow:**

  The full text is set as an HTML definition element with the abbreviation as ID to link to the first abbreviation usage.

  See [element IDs](/markup/element-ids) for the conversion of text to valid IDs.

  ```
  [::HTML: HyperText Markup Language]
  ```

  renders to

  ```html
  <dfn id="html">HyperText Markup Language</dfn> (

- **Other occurrences of the abbreviation:**

  ```
  [::HTML]
  ```

  renders to

  ```html
  <abbr>HTML</abbr>
  ```
