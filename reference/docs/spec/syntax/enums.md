# Enumerations
Enums are wrappers around integer types. They represent a finite set of possible values.
To define an enumeration, bicus uses `enum` keyword:
```
enum MyEnum {
  LOREM,
  IPSUM,
  HELLO,
  WORLD,
}
```
This will cause the compiler to treat this a an unsigned integer with minimum number of bits to hold all elements.
In the case above, compiler will treat this as `u2`, because we need 2 bits to hold `3` in binary (0-3).

We might also assign integer types to this enum, so that it is represented by what we want:
```
// Comments show what compiler assigns on its own.
enum(u16) MyEnum {
  LOREM, // = 0
  IPSUM = 3, // This is only possible if we provide our own integer type.
  HELLO, // = 4
  WORLD, // = 5
}
```

There is also a wildcard `_`, which makes an enum "non-exhaustive", meaning It can take any value from the inner type (u16 in example below):
```
enum(u16) MyEnum { A, B, _ }
```

Just like structures, enums can be used as anonymous types.
Possible attributes are the same as for structures.

Enum types can also be combined using special syntax: `EnumA & EnumB`, which will combine all variants from those enums into a new one.
