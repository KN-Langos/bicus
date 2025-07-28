# Literals
### Numeric Literals
Numeric literals can be in a few possible variants, all of which are listed below:
| Syntax | Description |
| ------ | ----------- |
| `[0-9][0-9_]*` | Integer literal |
| `[0-9][0-9_]*\.([0-9][0-9_]*)?` | Float literal |
| SCIENTIFIC NOTATION | TODO |
| `0x[0-9abcdef][0-9abcdef_]*` | Hex integer literal |
| `0b[01][01_]*` | Binary integer literal |

### String and Character Literals
Strings are composed of characters, which can be denoted using `'<char>'` syntax.
For example `'a'` will represent a character `a`.
Characters support `UTF-8`.

Strings are denoted with `"<content>"` syntax, and are represented with `std.String`,
so that `"Hello"` will be represented as `std.String.raw(&[72, 101, 108, 108, 111])`.
Slice in example above will be a static block of memory in a resulting executable.

Strings can also be prefixed to change their behavior. List of all prefixes is below:
| Prefix | Description |
| ------ | ----------- |
| `c` | Changes string representation from `std.String` to `*u8` and appending `\0` at the end. |
| `r` | Makes the string *raw*, by ignoring all escape sequences like `\n`, etc. |

### Template Literals
Template literals are also strings, but with a small quirk, being that it is possible to include variables in them.
They use ``` `<template>` ``` syntax, in which expressions are embedded using `{<value>[:<format>]}`.
If one wants to include `{` symbol in a template, use `{{` and `}}` (providing `\{` would be weird as closing it would not require `\`).

Available format specifiers are:
| Format | Description |
| ------ | ----------- |
| TODO | TODO |

### Struct Literals
Structures can be initialized by using explicitly typed syntax:
```
const first = MyStruct {
  field_a: 1,
  field_b: 5,
};
const second = MyStruct2(1, 5); // Tuple-like struct.
```
Or for those situations where type can be infered, Bicus also provides anonymous syntax:
```
const first: MyStruct = .{
  field_a: 1,
  field_b: 5,
};
const second: MyStruct2 = .(1, 5); // Tuple-like struct.
```
This is especially useful when using anonymous structs.

### Enum/Union Literals
Every enum field is a literal (constant) with an underlying value:
```
enum MyEnum {
  LOREM, IPSUM, HELLO, WORLD,
}
```
In an example above `MyEnum.LOREM` will be a value of type `MyEnum`.

Same as with structures, in a context where type might be infered, using `.LOREM` is also allowed and recommended.

For unions, there are few possible kinds of variants, so all of these are allowed depending on a variant:
```
union MyUnion {
  none, // Unit variant
  small(u16), // Single variant
  big(u64, u64), // Tuple variant
  complex { field_a: i32, field_b: bool }, // Struct variant
}

// Examples:
MyUnion.none
MyUnion.small(5)
MyUnion.big(1, 2)
MyUnion.complex { field_a: 1, field_b: true }
```

Of course shortcut syntax is still allowed, using `.tag`, `.tag(value)`, `.tag(a, b)`, `.tag { a: value, b: value }`

### Array and Slice literals
Arrays and slices can be defined using `[a, b, ...]` syntax, and `&[a, b, ...]` syntax respectively.

### Special literals
There are also some special literals, they are:
| Keyword | Description |
| ------- | ----------- |
| `true` | Returns boolean representing `true` value. |
| `false` | Returns boolean representing `false` value. |
| `undefined` | Represents an uninitialized value, in a safe mode bicus will track this and error if accessed (memory will be filled with `0xaa`). |
