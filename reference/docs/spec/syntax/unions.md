# Unions
Unions take `one of` multiple `variants`. Its size is the size of the largest variant.

## C-style unions
Basic unions do not keep track of which variant is active (except in safe compile mode, where compiler would tag them to avoid ub):
```
union MyUnion<generics>{
  none, // Unit variant
  small(u16), // Single variant
  big(u64,), // Tuple variant
  complex { field_a: i32, field_b: bool }, // Struct variant
}
```

Fields in unions are treated as structs, so they can be either tuple or struct variants, just like structures.
Accessing variants is done using member access syntax:
```
my_union_instance.none // Returns unit.
my_union_instance.small // Returns u16.
my_union_instance.big.0 // Returns u64.
my_union_instance.complex.field_a // Returns i32.
```

In safe mode accessing inactive variant will cause runtime error, while doing the same in fast mode will cause undefined behavior (UB).
Syntax of all these variants is the same as for structs, meaning that default values are also allowed.

## Tagged unions
It is recommended to avoid using C-style unions whenever possible, and use tagged unions instead.
Tagged unions under the hood are represented by `(Tag<T>, Value<T>)`, where `Tag<T>` is an enum, and `Value<T>` is C-style union.
They are defined with `tagged union` syntax:
```
tagged union Option<T>{
  some(T),
  none,
}
```
This will be represented by the compiler as the following:
```
union OptionValue<T> {
  some(T),
  none,
}

enum OptionTag {
  some, none
}

type Option<T> = (OptionTag, OptionValue<T>)
```

User does not have to interact with this structure, this is only an implementation detail.
Accessing tagged union values forces programmer to check for type validity. This can be done using any pattern match expression:
```
if match .some(value) = my_option_instance {
  // This will execute only if my_option_instance has a tag of `some`.
}
```

For cases, where accessing tagged union in an unsafe way is desired,
one can use compiler builtin `TODO`.

Matching tags can also be done using `builtin.tag(my_option_instance)` which returns `builtin.Tag<Option<T>>`.
