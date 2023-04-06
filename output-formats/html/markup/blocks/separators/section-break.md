# Section break

**WIP**

A section break has three different output variants for the HTML output format.

1. Used as column break inside an explicit column

  This is defined in the [explicit column](/output-formats/html/markup/blocks/enclosed/columns/explicit-column) section.

2. Used as page break with attributes

  All content up to the next page break is put inside a `div` block with the attributes set to the opening `div` tag.

  If a text group is opened, but not closed between page breaks, four `div` blocks are created in the following way:

  1. The first `div` block contains all elements until the text block start,
  and has the attributes of the first page break applied

  2. The second `div` block contains all elements between the text group start and the second page break, and has the attributes of the text group and first page break merged and applied with the text group attributes taking precedence

  3. The third `div` block contains all elements between the second page break and the text group end, and has the attributes of the text group and second page break merged and applied with the text group attributes taking precedence

  4. The fourth `div` block contains all further elements until a next page break, end of file, or a split page break text group constellation is reached again. The attributes of the second page break are applied.

3. Used as regular page break without attributes

  ```
  :::
  ```
  
  renders to 
  
  ````html
  <br/>
  ```
