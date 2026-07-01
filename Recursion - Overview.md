# Recursion - Overview

Recursion is a problem-solving method. In code, it's implemented as a function that calls itself. It's the counterpart to **iteration** (for loops / while loops) — any iterative algorithm can be rewritten recursively. Iteration uses loops to simulate repetition; recursion uses function calls to do the same.

## Example: print 1 to 10

**Iterative:**
```
for (int i = 1; i <= 10; i++) {
    print(i)
}
```

**Recursive (broken — no base case):**
```
function fn(i):
    print(i)
    fn(i + 1)
    return

fn(1)
```
Each call prints `i`, then calls `fn(i + 1)`. This never stops — it would print forever, because `fn(i + 1)` is called *before* `return`, so `return` is never reached.

This example is pretty pointless in practice — a for loop is simpler for just printing numbers. Recursion actually shines when a problem can be broken into smaller **subproblems** whose solutions combine to solve the original problem (see [[Recursion - Breaking Down Problems (Fibonacci)]]).

#dsa #algorithms #recursion

Related: [[Recursion - Base Cases]], [[Recursion - Call Stack and Execution Order]]
