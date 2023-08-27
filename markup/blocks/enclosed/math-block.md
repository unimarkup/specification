# Math block

Math blocks use `$` as keyword.

Math blocks allow using math mode on block level. Content inside a math block is treated as one mathematical formula.
Backslash escapes may be used inside render blocks as described in [/markup/escaping](/markup/escaping.md).

**Example using [AsciiMath](http://asciimath.org/):**

```
$$$
sum_(i=1)^n i^3=((n(n+1))/2)^2
$$$
```

**Type:** `math-block`

**Attribute:**

- `markup-syntax` ... Sets the name of the markup syntax that is used inside math formatting.

  **Note:** If the given name is not supported by the implementation, the text including the keywords must be treated as plain text.

**Note:** Implementations may allow additional attributes.
