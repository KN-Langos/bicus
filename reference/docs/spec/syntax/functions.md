# Function Definitions

Functions are defined starting with a keyword `func`.

Outlined syntax of the function looks like this:
```
func name<generics>(arg1: type, arg2: type = default_value) -> return_type {
    // Implementation
}
```

Return types may be omitted for simple cases where type inference is able to deduct the return type.
There is also shortcut syntax available that requires omitting the return type:
```
func add(a: i32, b: i32) => a + b;
```

Default values for arguments are allowed only at the end of argument list, so that those can be omitted in function call.

# Function Declarations
External functions can be declared with a `decl` keyword.
Such functions do not have a body, and are expected to be available during linking step:
```
decl "C" func add(a: i32, b: i32) -> i32;
```

Declaration above specifies an ABI (here "C" ABI).
This part of declaration can be omitted, which then defaults to "bicus" ABI,
which supports generics and non-c compatible structures/unions/etc.
