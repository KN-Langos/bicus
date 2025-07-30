# Closures

```
// We need to decide between one of these:
(a, b) => { ... }
(a, b) { ... }
|a, b| { ... }
func (a, b) { ... }
```

Closures are defined using `|args| <body>` syntax. `<body>` might be either a block or a single expression.

For function calls, if last argument is a closure, we allow trailing closure syntax:
```
func get<R: IntoResult>(*self, path: String, handler: |req: Request| -> R) { ... }

// In some other function:
var server = ...;
server.get("/") |req| `Hello {req.ip}!`;
```
