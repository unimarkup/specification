# Variables

;; mhatzl

## Flags

Flags are given in the [preamble](README.md) and provide the possibility to control the rendered output.
They may be used at the start of inline text groups, text blocks, or attribute blocks by setting `?` directly after the opening character.
Flags may contain any character except `?\&()` and spaces. A second `?` closes the flag section. 

Since flags represent a boolean condition, it is possible to combine several flags using boolean logic.
The logical formula is entered between the two `?`.

**Logical operations with flags:**

- **OR** ... `?flag1 | flag2?` means (flag1 OR flag2)
- **AND** ... `?flag1 & flag2?` means (flag1 AND flag2) 
- **NOT** ... `? !flag1 ?` means (NOT flag1)
- **Precedence** ... `?(flag1 & flag2) | flag3?` means (Either flag1 AND flag2, OR flag3)

**Usage:**

```
[?flag1? Text that gets rendered, if flag1 is set]
{?flag1? Attributes that are applied, if flag1 is set}

[?flag1 | (!flag2 & flag3)? Inline text block with logical formula]
```

