# Structures
Structures represent organized groups of values. They are defined with a `struct` keyword.

An example syntax of such definitions looks like this:
```
struct MyStruct<T> {
  field_a: T,
  field_b: usize = 5,
  some_other_field: bool,
}
```

Generics are described in a separate section of this specification.
Field `field_b` has a default value of `5`, which means It can be omitted when initializing this struct.

Structures can also be anonymous types, so that they can be inlined:
`struct { a: u32, b: u32 }`.

Structure definitions may also contain methods, which is useful for `with` clauses (look into traits section).
However, methods are allowed only after the last field of a struct.

Structures can also work as named tuples, by using `struct Name(i32, u32)` syntax.

There are a few attributes that are supported by structures, and those are:
- `@[repr = "C"]` - Sets ABI representation of this struct to be C compatible.
- `@[packed]` - Tells the compiler to pack values, even It it would mean lower performance.
For example structure defined with `struct { a: bool, b: bool }` would normally take 2 whole bytes of memory,
because each field would be aligned to a byte.
However, after using this attribute, this struct would only take 1 byte, as those 2 booleans will be packed into single bit each.
