# Attributes
Attributes are used to provide additional information to the compiler.

Every attribute is related to the following item, statement or expression, with its syntax looking like the following:
```
@[<attribute>]
// Item, statement or expression goes here...
```
There is also a special kind of attribute, that works from inside of module and looks like this:
```
@![<attribute>] // This must be the first thing in the module.
```

For both of these, `<attribute>` is one of three kinds:

### Marker attribute
Marker attributes are just identifiers, for example `@[inline]` before iterative loop, might tell compiler to
inline iterations at compile time.

### Call-style attribute
These attributes look like calls, taking positional arguments only.
One example of such attribute is a docstring, which looks like this `@[docstring("My docstring content")]`.

### Assignment-style attribute
These attributes look like assignment expressions. For example we might have something that looks like this:
```
[...]
@[rename = "myStructField"] my_struct_field, // Some kind of metadata for json parsing.
[...]
```

:::info
Compiler may introduce new attributes during any lowering step,
in order to provide metadata for the next pass.
:::
