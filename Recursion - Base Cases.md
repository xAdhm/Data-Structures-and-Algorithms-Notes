# Recursion - Base Cases

A **base case** is a condition at the start of a recursive function that stops the recursion. Without one, the function calls itself forever (see the broken example in [[Recursion - Overview]]).

## Fixed example: print 1 to 10

```
function fn(i):
    if i > 10:
        return

    print(i)
    fn(i + 1)
    return

fn(1)
```

Walkthrough of how it terminates:
- Calls proceed `fn(1) → fn(2) → ... → fn(10) → fn(11)`
- `fn(11)` triggers the base case (`i > 10`) and returns immediately
- Control returns to `fn(10)`, which moves to its own `return` line
- This "unwinds" back through `fn(9)`, `fn(8)`, ... down to `fn(1)`, and the whole thing terminates

**Rule of thumb:** every recursive function needs at least one base case, checked *before* the recursive call, or the recursion never stops.

#dsa #algorithms #recursion

Related: [[Recursion - Overview]], [[Recursion - Call Stack and Execution Order]]
