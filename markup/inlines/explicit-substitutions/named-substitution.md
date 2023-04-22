# Named substitutions

**WIP**

Named substitution may be used to replace a word by inline content.
For this, the word to be substituted must be enclosed by `::`.

**Note:** If whitespaces appear between `::` (more than one word between),
no substitution is applied. Therefore, substitutions are only possible per word.

[Emoji aliases](https://github.com/github/gemoji/blob/master/db/emoji.json)
must be predefined for substitution, substituting the alias with the respective Unicode code point.

To define new named substitutions, set `:` after the word to substitute, followed by the text that is used as substitution.

**Note:** The text to substitute must not start with `:`.

**Note:** The first substitution in document flow for a word must be used for all further substitutions. Ignoring all other substitution texts.

**Note:** If a substitution text is set for a word that already has a substitution, the implementation must output a warning.

**Usage:**

```
Standalone substitution: ::wink::

Inside a wo::smiley::rd

Custom substitution for: ::um: Unimarkup::
::um:: is a new markup language.
```

The above must be substituted to

```
Standalone substitution: 😉

Inside a wo😃rd

Custom substitution for: Unimarkup
Unimarkup is a new markup language
```

**Type:** `named-substitution`
