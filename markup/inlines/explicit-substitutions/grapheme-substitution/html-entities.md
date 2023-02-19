# HTML entities

There are several HTML entities defined in the HTML standard.
HTML entities have the general form `&<entity name>;` or `&#<entity number>;`.

In Unimarkup, the syntax is slightly modified to `&h+<entity name>;` and `&h+#<entity number>;`.

**Note:** The `h` must be interpreted case-insensitive, so `&H+<entity name>;` must also work.

**Note:** The entities for `gt`, `lt`, and `amp` must not be supported, since they are used to escaping HTML keywords.

**Usage:**

```
&h+euro;
```

This will render to

```
€
```

**Type:** `html-entity`
