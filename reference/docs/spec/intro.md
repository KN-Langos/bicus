---
sidebar_position: 1
---

# Introduction
This is a language specification for "Bicus" programming language.

## Syntax
Syntax is described in detail in its own category, but here are some simpler/general syntax elements:

### Comments
Bicus supports 3 following types of comments:

#### Line comments
Denoted with `//`, everything that follows until the end of line is considered a comment. <br/>
For example `some code // My comment!`.

#### Multiline/Inline comments
Sometimes comments need to span multiple lines, or be inside of let's say function call.
In such cases, this is the right comment kind.
Starting with `/*` and ending with `*/`, everything inside will be considered a comment. <br/>
For example:
```
/*
This is a comment.
And It has multiple lines!
*/
```

#### Docstring
Ignored during compilation, but useful for tools such as automatic docs generation.
Denoted with `//!` the following item will be considered a docstring.
For module-/internal-level docstring there is `///!`, that only works on top of given module.

This is actually just a syntax sugar for attribute `@[doc("Some docstring")]` for item docstring, and `@![doc("Some docstring")]` for module-level docstring.

### Items, statements, and expressions
We might divide every language element into three kinds: items, statements, and expressions.
Those are not fully separate, as one may contain the other.

#### Items
Items define some kind of reusable element. At this moment these include:
- Structures,
- Enumerations,
- Unions,
- Extensions,
- Function definitions,
- Function declarations,
- Imports.

#### Statements
Statements are all things that can be used in a context where there is no tracking of return value.
Examples of such things are conditionals, loops, and variable definitions.
Every code block is composed of statements with the following syntax: `{ statement* }`.

Depending on a context, items or expressions may become `item_statement` or `expr_statement` respectively.

#### Expressions
Expressions always return some kind of value (void/unit being considered a value).
This is the most common and largest element group.

## General Information
- Official file extension for source files is `.bri`.

#### Memory Management
Bicus will be a memory managed language, with a custom runtime that introduces Garbage Collection (GC).
First versions of Bicus will have a very primitive GC, while in the future we might move to generational or heuristic-based GC.

- traits
```
struct MyStruct { ... }

trait MyTrait {
    fn hello(self) -> int
}

impl MyTrait for MyStruct {
    fn hello(self) -> int {} # Required here
}

impl MyTrait for i32 {
    fn hello(self) -> int {} # Required here
}

struct AnotherStruct with MyTrait {
    fn hello(self) -> int {} # Required here
}

func something<T: MyTrait>(value: T)
func something(value: MyTrait)
func something(value: *dyn MyTrait) # With VTable

# Te dwa to to samo:
func something<T: MyTrait>(value: T)
func something(value: MyTrait)
# Jeśli funkcja `something` jest wywołana, to kompilator generuje osobną funkcje dla każdego typu który był użyty.
# Czyli:
something(1 as i32)
something(1 as u64)
# Wygeneruje 2 osobne funkcje: `something$i32` i `something$u64` z osobnymi implementacjami dla tych typów.

# A takie coś:
func something(value: *dyn MyTrait)
# Wygeneruje taką strukturę:
struct MyTraitVTable {
    inner: *any,
    hello: *fn(*any) -> int
}
# I potraktuje tą funkcję jako:
func something(value: MyTraitVTable)
# I wywoła np `something(5)` jako:
something(MyTraitVTable{
    inner: &5,
    hello: &MyStruct.hello
})

```