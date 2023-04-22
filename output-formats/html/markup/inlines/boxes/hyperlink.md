# Hyperlink

There are two variants:

- **Link is a URLs**

  ```
  [GitHub](https://github.com)
  ```

  renders to

  ```html
  <a href="https://github.com">GitHub</a>
  ```

- **Link is a relative path**

  The implementation may choose the rendered output.  
  This allows handling [routing](https://reactrouter.com/en/main), as used in common web frameworks like [React](https://react.dev/), with the same syntax as regular links.
