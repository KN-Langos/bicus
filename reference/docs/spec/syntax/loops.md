# Loops
Most basic type of loop uses keyword `loop`. It is works like `while (true)` in other programming languages:

```
loop {
  // Do something here.
}
```

Combined with `break` and `continue` this is technically the only necessary loop, but for convenience we also provide `while` and `for` loops:

While loops allow programmer to check condition every time a loop is being called:
```
while condition {
  // do something here.
}
// Above is equivalent to:
loop {
  if !condition { break; }
  // Do something here.
}
```
As with conditionals, there is also special `while match` statement, that works until given pattern failes to match.

For loops are more complex, and require something that implements `core.iter.IntoIterator` trait,
which is implemented by default for every type implementing `core.iter.Iterator` trait.

Many core types implement this, for example ranges implement `IntoIterator`, which makes them `RangeIterator` with integer type item:
```
for i in 0..8 {
  // Do something here.
}
// Above is equivalent to:
var _iter: core.iter.Iterator<Item=u32> = 0..8.into_iterator();
var _i: Option<u32> = _iter.next();
loop {
  if match .none = _i { break; }
  const .some(i) = _i; // else unreachable; might be necessary in stage 1 as we will not track possible variants yet.
  // Do something here.
  _i = _iter.next();
}
```
In the provided example `i` can be replaced by any pattern that can be matched by any element of type `Iterator.Item` (same as with function parameters).
