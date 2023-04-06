# Text box

There are two variations:

1. No attributes set

   If no attributes are set for an inline text group, the text is taken as is without surrounding it with any HTML tag.

   ```
   outside text [*plain* text group]
   ```
   
   renders to
   
   ```html
   <p>outside text *plain* text group</p>
   ```

2. Attributes set

   Text attributes are converted to style properties.

   ```
   [text group]{<some attributes>}
   ```
   
   renders to
   
   ```html
   <span style="<converted attributes>">text group</span>
   ```
