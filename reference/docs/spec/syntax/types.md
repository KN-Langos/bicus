# Types
### Primitive types
There are some types that cannot be broken down into smaller parts.
Those are primitives, which bicus defines internally:

| Type | Description |
| ---- | ----------- |
| `i<size>` | Signed integer with `<size>` bits. |
| `isize` | Pointer-sized signed integer. |
| `u<size>` | Unsigned integer with `<size>` bits. |
| `usize` | Pointer-sized unsigned integer. |
| `f<size>` | Floating point number with `<size>` bits. Supports only sizes of `16`, `32`, `64`, `80`, `128`. |
| `bool` | Logical value that can be either `false` or `true`. This is essentially an `i1`. |
| `char` | Represents a single character of a string. This is unicode compatible, and has size of 21 bits. |
| `unit` | Similar to `void` in some languages. this is a zero-sized value. |
| `never` | Tells the compiler that given function will never return. Useful for `panic` and infinite loops. |

### Error types
Errors are implemented as tagged unions:
```
tagged union Result<T, E>{
    ok: T,
    err: e,
}
```

### Optional types
Optional types are also tagged unions:
```
tagged union Option<T, E>{
    some: T,
    none,
}
```

### Other types
There are also other special types that are `composites`, and can be broken into smaller parts:

| Type | Description |
| ---- | ----------- |
| `*<T>` | Single-element pointer. This represents pointer to a value of type `<T>`. |
| `*any` | Special kind of single-element pointer. This is a pointer of unknown type, similar to `*void` in some languages. |
| `[<n>]<T>` | Arrays with given size. They represent `<n>` contiguous elements of type `<T>` in memory. |
| `[*]<T>` | Multielement pointer. Tells the compiler that this is the first element of unknown-sized array of `<T>`. |
| `[]<T>` | Slice. Represents a multielements pointer with a length. It is something like `(usize, []<T>)` under the hood. |
| `(<T1>, ..., <TN>)` | Tuple. This works like an anonymous structure with fields named `0..N`, etc. |

Note: In a safe mode `*any` will store info about which type it holds to avoid UB.
