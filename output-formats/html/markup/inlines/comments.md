# Comments

The behavior depends on the configuration option `keep-comments`.

- Option set

  Comments are converted to HTML comments.

  ```
  ;; comment to end of line
  ```

  renders to

  ```html
  <!--comment to end of line-->
  ```

  **Note:** Special HTML keywords must also be replaced in comments.

- Option **not** set

  Comments are not forwarded to the resulting output file.
