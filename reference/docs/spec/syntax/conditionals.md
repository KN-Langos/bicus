# Conditionals
Conditionals are used to change the way code flows during execution.

Bicus supports standard `if-else`, which can also be used as an inline expression.
Standard if else looks like the following:
```
if <condition> {
  ...
} else if <condition> {
  ...
} else {
  ...
}
```
Of course `else` part might be omitted, in which case nothing will happen if condition does not return true.

For more complex needs there is also `if match`, which uses the following syntax:
```
if match <pat> = <value> {
  ...
}
```
This syntax is especially useful for checking if option is `some` or whether an error has ocurred.

There is also an inline variant of conditional, which can be used as expressions:
```
const result = if <condition> then "true" else "false"; // "then" kw is required to tell where `condition` ends.
```
