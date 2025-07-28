# Match Expression
Match statements use patterns, so for those please refer to the `Patterns` section.

Match expressions are like switches. They allow for multiple branches in a single block.
Every pattern with its corresponding block of code is called an `arm`.

Here is an example of a match expression:
```
match x {
  0..=5 => /* Do something */,
  _ => { /* ignore */ },
}
```
This is an expression, meaning it can return a value, however all arms must have the same return type.

For cases such as integers, enums, unions, and other, compiler requires all possible values to be covered,
so if omitting one variant is desired, just use `_ => {}` to ignore remaining values.
