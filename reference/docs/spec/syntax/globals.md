# Globals/Statics
You can define a static global variable using `static` keyword:
```
static NAME: type = value;
```

If value resolves to a compile-time known value and is never mutated in the source, It will be put as a constant.
In every other case It will be part of `constant initialization` in runtime.
