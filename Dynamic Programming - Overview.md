# Dynamic Programming - Overview

**Dynamic programming (DP)** is a problem-solving technique — many problems solvable with DP genuinely can't be solved any other way in reasonable time complexity. DP has a reputation as the most-feared topic, partly because it's nearly impossible to solve a DP problem without already knowing DP (even "easy" ones), and partly because it's less universally emphasized in interviews.

## The core idea: DP is optimized recursion
Same idea used throughout [[Binary Trees - DFS Overview|tree DFS]]: define a recursive function (there, `dfs`; here, usually `dp`) that returns the answer to the **original problem**, treating whatever arguments it's called with as the input. In tree problems, `dfs(node)` answered "what's the result for the subtree rooted at `node`." In DP, `dp(state)` answers "what's the result treating `state` as the input."

## The key difference from tree recursion: repeated states
In tree DFS, a node was **never visited twice** — no repeated states. In DP, **the same state can recur** — often an exponential number of times — which is precisely the inefficiency DP exists to eliminate.

## Memoization: the fix for repeated states
Cache the return value for each state the first time it's computed (usually in a hash map). If the same state is ever needed again, look it up instead of recomputing. Same idea introduced for [[Graphs - DFS Implementation Differences from Trees|graph traversal's `seen` set]] — and just as with graphs, if the range of possible states is known upfront, an **array** can be faster than a hash map for caching in some languages.

## Worked example: Fibonacci
`F(n) = F(n-1) + F(n-2)`, with `F(0)=0`, `F(1)=1`. This formula is called a **recurrence relation**.

### Naive recursion — O(2ⁿ)
```python
def fibonacci(n):
    if n == 0:
        return 0
    if n == 1:
        return 1

    return fibonacci(n - 1) + fibonacci(n - 2)
```
Every call spawns 2 more calls → exponential blowup. In the recursion tree for `fibonacci(6)`, `f(4)` gets computed twice, `f(3)` three times, `f(2)` five times — and this redundancy compounds fast as `n` grows (the tree for `f(7)` is roughly twice the size of `f(6)`'s).

### Adding memoization — O(n)
```python
def fibonacci(n):
    if n == 0:
        return 0
    if n == 1:
        return 1
    if n in memo:
        return memo[n]

    memo[n] = fibonacci(n - 1) + fibonacci(n - 2)
    return memo[n]
memo = {}
```
Checking the cache before recursing eliminates all the redundant recomputation — this single change is what turns "basic recursion" into "dynamic programming." O(2ⁿ) → O(n) is an enormous improvement.

See [[Dynamic Programming - Top-Down vs Bottom-Up]], [[Dynamic Programming - When to Use It]], and [[Dynamic Programming - State]] for the rest of this article's concepts.

#dsa #algorithms #dynamic-programming #recursion

Related: [[Recursion - Overview]], [[Binary Trees - DFS Overview]], [[Graphs - DFS Implementation Differences from Trees]]
