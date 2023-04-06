# Attribute block

**WIP**

Every attribute block is converted to CSS.
If the block was set in nested context, the ID of the parent element is set before every top-level selector in the block.
However, the parent ID must not be set as selector if the attribute block is returned from a macro, or memorable.
This allows to define different themes, and insert them as needed. 

**Note:** The converted CSS should be placed in the `head` HTML section for better rendering performance. 
