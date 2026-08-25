# Dynamic Programming - Top-Down vs Bottom-Up

Two ways to implement a [[Dynamic Programming - Overview|DP]] algorithm.

## Top-down
Recursion + memoization (as shown in [[Dynamic Programming - Overview]]'s Fibonacci example). Called "top-down" because it starts from the top — the original problem (e.g. `fibonacci(n)`) — and recurses **down** toward the base cases (`F(0)`, `F(1)`).

## Bottom-up (tabulation)
Start at the base cases and iteratively build **up** toward the target answer.

```python
def fibonacci(n):
    arr = [0] * (n + 1)
    # base case - the second Fibonacci number is 1
    arr[1] = 1
    for i in range(2, n + 1):
        arr[i] = arr[i - 1] + arr[i - 2]

    return arr[n]
```

## They're fundamentally the same algorithm
Top-down and bottom-up are purely an **implementation choice** — there's nothing fundamentally different between them. Every top-down solution can be rewritten bottom-up and vice versa. What actually **defines** a DP algorithm is its base cases and recurrence relation (covered in more depth in a later article) — not which direction it's implemented in.

## Tradeoffs
- **Bottom-up is usually faster** — iteration has less overhead than recursion (though less true in languages with tail-call optimization).
- **Top-down is usually easier to write** — with recursion, the order states get visited doesn't need to be manually figured out. With bottom-up iteration on a **multi-dimensional** problem, correctly nesting/ordering `for` loops so every dependency is computed before it's needed can be genuinely tricky.

#dsa #algorithms #dynamic-programming

Related: [[Dynamic Programming - Overview]], [[Dynamic Programming - State]]
