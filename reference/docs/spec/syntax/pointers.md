# Pointers

Bicus is a garbage collected language, so pointers will be freed automatically after they are no longer in use.
To get a pointer to a value one might use `&` prefix unary operator, which returns pointer to an underlying value.
In a case where given value is on a stack (not static), but needs to escape the current frame (let's say function return),
Bicus will automatically allocate It on the heap using default allocator.
