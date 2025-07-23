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

## General information
- Official file extension for source files is `.bri`.
- Memory management: TODO.
