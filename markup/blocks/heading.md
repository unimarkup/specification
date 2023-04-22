# Heading

Headings are set in [atx-style](http://www.aaronsw.com/2002/atx/intro) with support for 6 heading-levels.

A `#` at start of a line followed by one space marks a heading.
Adding more `#` before the space increases the heading-level.
The heading text starts after the space and may contain any inline content.

For multiline heading text, the following lines must either start with the same heading level, or any grapheme except `#`.

Another heading that is one heading-level lower may be set directly on the next line, without the need for a blank line.

Attributes may be used at the end of the heading text.

**Note:** If not set manually, IDs must be created implicitly for headings, by setting Latin graphemes to lower case, spaces between graphemes must be replaced by `-`, and other graphemes besides numbers and Latin graphemes must be removed.
If the resulting ID is already present in the document, the ID may be freely chosen by the implementation,
but a warning must be output.

**Usage:**

```
# First main heading

Some Unimarkup text for this heading...

## Nested heading

More unimarkup text for the nested heading...

# Second main heading
## Other nested heading

Even more Unimarkup text...
Reference to the first heading [##first-main-heading]

# Heading with attributes
{<heading attributes>}

# Multiline
# heading is also possible

The first paragraph of this heading level starts here.

# Multiline heading with
  additional attributes{<heading attributes>}

# Heading with explicit identifier
{ id: explicit-heading-id }
```

**Examples of invalid headings:**

- Wrong heading level of follow-up heading

  ```
  # Heading
  ### Bad follow-up heading
  ```

- No blank lines before

  ```
  Some text...
  ## No blank lines before heading
  ```

- No space after `#`

  ```
  #No space between # and heading text
  ```

**Types:**

All headings are subtypes of the `heading` type.
Each heading has its own type `heading-<heading level>`.
