# Traits
Traits define common methods that can be implemented by other types.
They basically extend existing types with new things.

They are defined using `trait` keyword like the following:
```
trait Greetable {
  // This requires every implementor to have this method available.
  func greet(self) -> String;
}
```

Traits can also define default implementations that rely only on known values or compile-time reflection.
Generic types can also be applied to traits, so `trait MyTrait<T> { ... }` is possible.

Associated types are also available. One can think of them as output types of a given trait.
For example we might define the following trait:
```
trait Container {
  type Item;

  fn contains(*self, item: *Self.Item) -> bool;
}
```
This improves code readability of methods and structures that can accept any `Container`:
```
// Without associated types
func has<C: Container<Item>, Item>(container: *C, value: *Item) -> bool { ... }

// With associated types
func has<C: Container>(container: *C, value: *C.Item) -> bool { ... }
```

For simplicity traits may be defined not only using the `extend` keyword (refer to the `Extensions` section),
but also using `with` clause, which can be applied to structures, enums, and unions.
For example we might define our structure using `struct MyStruct with MyTrait { ... }`, which will require
this definition to contain all methods and associated types of a given trait.

Traits can be used as types in two ways, depending on a context and programmer's intent.
If neither of those is suitable in a given situation, please use generics with trait bounds.

#### Monomorphized static types
First way of using traits as types is denoted using just `TraitName` or `*TraitName`.
This is allowed only in function parameters, and will be treated the same way as trait bounds are:
```
func lorem(value: TraitName) => ...;
// The above will be the same as this:
func lorem<T: TraitName>(value: T) => ...;
```
This causes function to be monomorphized (split into multiple functions by the compiler), but does not allow
explicit types in calls, so It will not allow calls using `lorem.<i32>(5)` nor getting a function pointer.

#### Virtual dispatch types
Second way is denoted using `*dyn TraitName` syntax, and requires type to be a pointer.
This is allowed in every context, and will reference a virtual table of a given implementor.

This is a bit technical, so for more details please refer to the `Internals` section.
It does not affect how functions are called.
