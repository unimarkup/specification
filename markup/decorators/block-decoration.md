# Block decoration

Blocks may allow decoration to set additional information.
Each supporting block must define how this information may be formatted.

A block decoration has a similar syntax to [enclosed blocks](/markup/blocks/enclosed/README.md),
and uses `+++` as keyword.
The decoration must be set in the next line after the block ends, without any blank lines between.

**Note:** If attributes are set, the decoration must be placed after the attributes are closed.

**Example:**

```
!![Some image that turns into a figure by decorating it](myImg.png)
+++
Some figure description.
+++

===
| some | table |
===
+++
Awesome table description.
+++
```
