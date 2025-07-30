# Defer
Many modern languages opt into something we call "defer statement".
It tells the compiler to inline given statement at every possible exit path of a given block of code.

In Bicus, we use `defer` keyword for this, followed by any statement:
```
func abc() i32 {
  var x = 1;
  defer print(x); // Assume `print` is defined globally.

  if x == 1 {
    x = 2;
    // Defer will be called and will print 2.
    return x;
  }
  // Defer will be called and will print 1.
  return x;
}
```

This is useful for debugging, native calls that require destruction of parameters, and more.
