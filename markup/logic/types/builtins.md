# Builtins

This section contains all builtin types that are not Unimarkup elements.

**WIP**

## Bool

**Values:** `true`, `false`

**Note:** Both values are case-insensitive.

## Number

Parent type of all number types.

### Integer

**Values:** All values of the integer set.

**Note:** The smallest and biggest supported integer may be implementation dependent.

**Note:** Type `int` is an alias for `integer`.

### Natural

**Values:** All values of the natural set.

**Note:** The biggest supported natural may be implementation dependent.

**Note:** Type `nat` is an alias for `natural`.

### Real

**Values:** All values of the real set, with `.` used as decimal point.

**Note:** `1` is of type `int`, while `1.0` is of type `real`.

**Note:** The smallest and biggest supported real may be implementation dependent.

## Grapheme

**Value:** Represents one Unicode grapheme.

## Word

**Value:** Represents one Unicode word.

**Note:** This depends on the set locale while rendering.

## Range

Specifies an ascending integer range.
Assigned values may only be inside this range.

```
1..=2
```

```
1 ..< 2
```

## `Option<T>`

**Values:** `Some(T)`, `None`

## `Result<T1, T2>`

**Values:** `Ok(T1)`, `Err(T2)`

## File/Folderpath

**Value:** Valid file/folderpath for the used OS.
