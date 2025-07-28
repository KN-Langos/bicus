# Patterns
Patters are core of Bicus' syntax.
They allow for matching, destructuring, and many other.

Here are all possible patterns available in bicus:
| Pattern | Name | Description |
| ------- | ---- | ----------- |
| `_` | Wildcard | Matches anything and discards the value. |
| `<ident>` or `<ident> @ <pat>` | Binding | Binds identifier to a given value. If subpattern is provided it will bind only if it also matched. |
| `*<ident>` | Pointer | Same as binding, but identifier will be bound to a pointer to a value instead. |
| `.<tag?>{ x, y, .. }` or `Name { x, y, .. }` | Struct | Binds fields of a struct-type value. Supports "rest" syntax with `..`. `x` and `y` are also patterns. Allows for an optional tag, in which case it will work just like `.{ .. } @ .<tag>`|
| `.<tag?>(a, ..)` or `Name(a, ..)` | Tuple Struct | Same as "Struct" variant, but mathes tuple-like structures. `a` is also a pattern. Allows for an optional tag, same as above. |
| `.<variant>` | Enum Variant | Checks if given enum has active variant `<variant>`. Works also for unions, by default discards all values. |
| `(a, b, ..)` | Tuple | This works for normal tuples, useful for destructuring. If single value is desired use `(a,)`. |
| `<start?>..<end?>` or `<start?>..=<end?>` | Range | Checks if integer is between `<start>` and `<end>`. If one value is omitted it will check for beginning/end only. |
| `[a, b, ..]` | Slice | Matches an array, allows for `..` rest syntax. `a` and `b` are also patterns. |
| `(<pat>)` | Group | Used to group patterns together, useful for deeply nested patterns. |
| `<pat> if <guard>` | Guard | Matches pattern `<pat>` only if `<guard>` expression return `true`. |

We know this part can be a bit confusing, so here are some examples of patterns in action:

TODO
