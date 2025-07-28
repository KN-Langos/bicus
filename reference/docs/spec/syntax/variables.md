# Variables

Variables are defined using either `const` or `let` syntax (TODO: Discuss keywords).
Example of this definition syntax looks like the following:
```
const x = 1; // x will be 1 as u32.
const y: u16 = 5; // x will be 5 as u16.
let z = "Hello"; // z will be of type `String`.
```

If there is a need to keep variable uninitialized at the beginning, use `undefined` literal.
However, this works only with `let` definitions.
```
let value = undefined; // Will result in random memory in fast mode, and `0xaa` in safe mode.
```
