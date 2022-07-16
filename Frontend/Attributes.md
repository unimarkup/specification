# Attributes

Attributes may be set for elements using attribute blocks with attributes being in [JSON-Format](https://www.json.org/json-en.html).
There are general attributes that are valid for all Unimarkup elements and some specific ones for certain elements.
The position where an attribute block may be set for an element is described for each element or element group.

To reset attributes to their default values, write `""` for single value elements, `[]` for arrays and `{}` for objects.
If attributes are not set, default values are used, but resetting may be useful, if some parent changed attribute values that would be inherited.

## Attribute block

An attribute block is opened with `{` and closed with `}`.
The allowed positions of attribute blocks is defined in the attribute section of each element definition.
The attribute format, attribute groups and hierarchy are described in the [attributes section](#attributes). 

**Note:** Any `{` must be closed with `}`, if `{` opens an attribute block. Otherwise, rendering must fail.

**Usage:**

```
## heading
{<heading attributes>}

Paragraph text with `**verbatim**`{ "language" : "unimarkup" }
{<paragraph attributes>}
```

**Type:**

: `attribute` :
:-- `Single`
:
: Element type for element attributes.

## Attribute block concatenation

It is possible to concatenate attribute blocks, by starting another attribute block directly after closing one.
Attributes are taken from the left most attribute block and are overwritten by attributes of following attribute blocks,
if both attribute blocks are taken.

**Note:** A new line between concatenated attribute blocks is not allowed, but none breaking spaces are. 

**Example:**

- Using different flags for attribute blocks

  ```
  ## heading
  {?pdf? "color" : "rgb(0,255,0)" }{?html? "color" : "rgb(255,0,0)" }
  ```

- Using a base attribute block followed by a flagged attribute block

  ```
  # heading with text color blue and red background for the html output
  { "color" : "rgb(0,255,0)" }{?html? "background" : { "color" : "rgb(255,0,0)" }}
  ```

- Attribute overlapping

  ```
  # heading with in general blue text color except for html output, where it is red
  { "color" : "rgb(0,255,0)" }{?html? "color" : "rgb(255,0,0)" }
  ```

  **Note:** The following will always generate red text color!

  ```
  # heading with red text color (html attribute is overwritten)
  {?html? "color" : "rgb(0,255,0)" }{ "color" : "rgb(255,0,0)" }
  ```

## General attribute units

Since attributes are defined in JSON-format, there are objects with elements that may have the same attribute units.

**List of general attribute units:**

- `"<color unit>"`

  It is possible to set colors using

  - `rgba(<0-255>,<0-255>,<0-255>,<0.0-1.0>)` in the form `red, green, blue, alpha`
  
  - `rgb(<0-255>,<0-255>,<0-255>)` where alpha is set to `1.0`

  - `#RRGGBBAA` in hexadecimal values from `00` to `FF` for `RR` red, `GG` green, `BB` blue and `AA` alpha
  
  - `#RRGGBB` in hexadecimal values where alpha is set to `FF`

  - `hsla(<0-360>,<0-100%>,<0-100%>, <0.0-1.0>)` in the form `hue, saturation, lightness, alpha`

  - `hsl(<0-360>,<0-100%>,<0-100%>)` where alpha is set to `1.0`

  Alpha refers to the transparency value with `1.0` and `FF` having no transparency.

- `"<size unit>"`

  Size units are used to define the height or width of an element. A size is given as a decimal value followed by a unit abbreviation (e.g. `16pt`, `1.5em`, `10mm`).
  
  There are two main categories of size units:

  - Absolute units

    - `cm` ... Centimeter
    - `mm` ... Millimeter
    - `in` ... Inch (2.54 cm)
    - `pt` ... Point (1/72 inch)

  - Relative units

    - `em` ... Relative to the font-size of the element (2em = 2 times the size of the current font)
    - `rem` ... Relative to the base font-size of the document
    - `%` ... Relative to the size of the parent element
    
## General attributes

- `"class" : [ "class-name-1", "class-name-2", ... ]`

  Classes that may be used to provide attributes for different elements.

- `"padding" : { }`

  Define the space being added between the content and border of an element using padding.

  - `"all" : "<size unit>"`

    Applies the same padding to all four sides.

  - `"top" : "<size unit>"`

    Applies the padding to the top side overwriting `all`.

  - `"bottom" : "<size unit>"`

    Applies the padding to the bottom side overwriting `all`.

  - `"left" : "<size unit>"`

    Applies the padding to the left side overwriting `all`.

  - `"right" : "<size unit>"`

    Applies the padding to the right side overwriting `all`.

- `"margin" : { }`

  Define the space being added between the border of an element and the outer frame where other element frames start using margin.

  - `"all" : "<size unit>"`

    Applies the same margin to all four sides.

  - `"top" : "<size unit>"`

    Applies the margin to the top side overwriting `all`.

  - `"bottom" : "<size unit>"`

    Applies the margin to the bottom side overwriting `all`.

  - `"left" : "<size unit>"`

    Applies the margin to the left side overwriting `all`.

  - `"right" : "<size unit>"`

    Applies the margin to the right side overwriting `all`.
  
- `"border" : { }`

  Set a border for an element. 

  - `"radius" : { }`
 
    Border-radius of an element.

    - `"all" : "<size unit>"`

      Applies a radius to all four corners.

    - `"top-left" : "<size unit>"`

      Applies a radius to the top left corner overwriting `all`.

    - `"top-right" : "<size unit>"`

      Applies a radius to the top right corner overwriting `all`.

    - `"bottom-left" : "<size unit>"`

      Applies a radius to the bottom left corner overwriting `all`.

    - `"bottom-right" : "<size unit>"`
 
      Applies a radius to the bottom right corner overwriting `all`.

  - `"all" : { }`

    Border attributes that apply to all four sides.

    - `"color" : "<color unit>"`

      Border-color of an element.

    - `"style" : "<border style option>"`

      Border-style with the following options:

      - `none` ... no border
      - `dotted` ... dotted border `......`
      - `dashed` ... dashed border `------`
      - `solid` ... solid border `______`
      - `double` ... double border `======`

    - `"width" : "<size unit>"`

      Border-width of an element.

  - `"top" : { }`

    Attributes for the top border. Overwrites the values of `all`.
    Same attributes of `all` are available.

  - `"bottom" : { }`

    Attributes for the bottom border. Overwrites the values of `all`.
    Same attributes of `all` are available.

  - `"left" : { }`

    Attributes for the left border. Overwrites the values of `all`.
    Same attributes of `all` are available.

  - `"right" : { }`
 
    Attributes for the right border. Overwrites the values of `all`.
    Same attributes of `all` are available.

  - `"image" : { }`

    An image may be set as border.

    - `"source" : "<url to border-image>"`

      URL where to find the border-image.

    - `"width" : "<size unit>"`

      Width of the border-image.

    - `"scale" : "<border scale option>"`

      Define how an image is scaled, if it does not fill the complete border.

      - `"stretch"` ... The image is stretched to fill the border
      - `"repeat"` ... The image is repeated to fill the border

- `"background" : { }`

  The background object has several values. If a value is not set, the parent value is taken (At document level, the parent value is the default value).

  - `"color" : "<color unit>"`

    The background-color of an element.

  - `"image" : [ "<url to image1>", "<url to image2>", ... ]`

    One or more images that are used as backgrounds. Replaces the background-color.

## Text attributes

Text attributes provide attributes for text styling.

- `"font" : ["<font family1>", "<font family2>", ...]`

  Several font families may be set. The first font that is available starting from left is taken. It is also possible to provide generic font family names and a matching available font is then used.

- `"size" : "<size unit>"`

  The text-size.

- `"weight" : "(100|200|300|400|500|600|700|800|900)"`

  Adds a weight to the text overwriting inline formatted **bold**.

  The value `100` means very light characters and `900` very bold.
  `400` is for normal characters and `700` is the default for **bold**.  

- `"italic" : "(true|false)"`

  Sets the text as italic when `true` is set.

- `"color" : "<color unit>"`

  The text-color.

- `"spacing" : { }`

  - `"character" : "(<size unit>|kerning)"`
  
    Define the spacing between characters. `kerning` uses character spacing information from fonts that provide it.

  - `"word" : "<size unit>"`

    Define the spacing between words.

- `"line-height" : "<size unit>"`

  The vertical line height where the text is centered in the middle.

- `"alignment" : "<alignment option>"`

  The alignment of a text may have the following values:

  - `left` ... text is aligned to the left
  - `right` ... text is aligned to the right
  - `center` ... text is centered
  - `justify` ... every line has the same width

- `"align-last" : "<alignment option of last line>"`

  Define how the last line is aligned, if the text alignment is set to `justify`.
  Otherwise, `align-last` has the same option as `alignment`. 

  Possible options are:

  - `left` ... last line is aligned to the left
  - `right` ... last line is aligned to the right
  - `center` ... last line is centered
  - `justify` ... last line has the same width as previous text lines

- `"line-decoration" : { }`

  This attribute defines the line appearance that may be set for a text like underline, overline and strike through.

  - `"color" : "<color unit>"`

    Sets the line-color. If not set explicitly, the text-color is used.

  - `"style" : "<line styling option>"`

    Possible line styles are:

    - `solid`
    - `double`
    - `dotted`
    - `dashed`
    - `wavy`
    
- `"first-indent" : "<size unit>"`

  Size of the indentation of the first line of a text.

- `"justify-method" : "<justify method option>"`

  Defines the justification method used for `justify` alignment.

  Possible options are:

  - `auto` ... The best method is automatically determined
  - `inter-word` ... Increases/Decreases spacing between words

    **Note:** This overwrites the `word` attribute in the `spacing` object.

  - `inter-character` ... Increases/Decreases spacing between characters

    **Note:** This overwrites the `character` attribute in the `spacing` object. 

- `"word-break" : "<(true|false)>"`

  `word-break` defines, if a word may be broken at any character at the end of a line (`true`) to prevent an overflow, or if words may't be broken up (`false`).

## Block attributes

- `"id" : "<identifier name>"`
  
  The identifier name must contain at least one character, may not start with a number, and must not contain whitespaces.
  The name is case-sensitive and must be unique in the generated document.
  (The same constraints as with the [HTML ID attribute](https://www.w3schools.com/html/html_id.asp))

  **Note:** If several Unimarkup files are combined, the identifier name must be unique across all.

- `"ref" : { }`
  
  - `"label" : "<paragraph>"`

    The given paragraph may be used when referencing this element.

  - `"prefix" : "<paragraph>"`

    It is possible to set or remove a paragraph for elements, which would be prefixed when referenced.

## Attribute hierarchy

Different attributes may be applied at every level. If there are overlapping attribute values, the most local one is taken.
