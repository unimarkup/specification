# Text box

The text box is the most basic box element.

**Type:** `text-box`

This element has two use cases:

1. To apply attributes to inline content

    **Example:**

    ```
    A paragraph with [grouped text]{ font-size: 20pt }. Also grouping within one w[or]{ color: green }d is possible.
    ```

2. As verbatim alternative without a monospaced font

    This is achieved, by not setting attributes after `]`.
    The content inside the box is then taken as plain text.

    **Example:**

    ```
    [Text *group*] without attribute block => no formatting applied inside the text group.
    ```
