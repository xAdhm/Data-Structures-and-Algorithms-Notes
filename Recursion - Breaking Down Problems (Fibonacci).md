# Recursion - Breaking Down Problems (Fibonacci)

Recursion is most useful when a problem can be broken into smaller **subproblems**, whose solutions combine to solve the original problem — rather than just simulating repetition (see the pointless printing example in [[Recursion - Overview]]).

## Fibonacci numbers
Sequence: 0, 1, 1, 2, 3, 5, 8, ... where each number is the sum of the previous two.

**Recurrence relation:**
Fₙ = Fₙ₋₁ + Fₙ₋₂

A recurrence relation is an equation connecting terms of a sequence to earlier terms.

**Base cases:** F(0) = 0, F(1) = 1 (explicitly defined, not derived from the recurrence)

## Pseudocode

```
function F(n):
    if n <= 1:
        return n

    oneBack = F(n - 1)
    twoBack = F(n - 2)
    return oneBack + twoBack
```

## Trace of F(3)

```
oneBack = F(2)
    oneBack = F(1)
        F(1) = 1
    twoBack = F(0)
        F(0) = 0
    F(2) = oneBack + twoBack = 1
twoBack = F(1)
    F(1) = 1
F(3) = oneBack + twoBack = 2
```

F(3) breaks down into two smaller subproblems, F(2) and F(1). Each of those breaks down further until hitting base cases, then the results combine back up to solve the original problem.

## The general pattern
This is the most common recursion use case: design the function to **return the answer to the problem** for a given input. To implement it:
1. Identify the base case(s) — the simplest input(s) you can answer directly
2. Identify the recurrence relation — how to express the answer for input `n` in terms of answers for smaller inputs

Once both are defined, solving any subproblem is automatic — e.g. F(100) is just F(99) + F(98), and each of those recursively resolves the same way.

#dsa #algorithms #recursion #fibonacci

Related: [[Recursion - Overview]], [[Recursion - Base Cases]]
