# Dynamic Programming - State

**State** = a set of variables that fully describes a scenario. Introduced earlier for [[Binary Trees - DFS Overview|tree DFS]] — every `dfs(node, ...)` call's arguments represented the state. Same idea in [[Dynamic Programming - Overview|DP]]: `dp(state)` returns the answer to the original problem *as if* `state` were the actual input. Deciding on the right state variables is the **first step** in designing a DP algorithm.

## Common state variables to consider
- **An index along an input string/array/number.** The single most common state variable — appears in almost every DP problem, often as the *only* one. In Fibonacci, the "index" is which Fibonacci number you're computing. For an array/string, this typically represents "everything up to and including this index" as the effective input — e.g. `nums = [0,1,2,3,4]` with state `i = 2` behaves like the input were just `[0,1,2]`.
- **A second index**, when a **right bound** is also needed — e.g. `i=1, j=3` on `[0,1,2,3,4]` represents considering only `[1,2,3]`.
- **Explicit numerical constraints from the problem** — e.g. "you may remove `k` obstacles"; the state variable tracks how many removals remain.
- **A boolean status flag** — e.g. "currently holding a package or not."

## Dimensionality
The number of state variables used = the **dimensionality** of the algorithm. One variable (e.g. just `i`) → one-dimensional. Multiple state variables → multi-dimensional. Some problems need as many as 5 dimensions.

#dsa #algorithms #dynamic-programming

Related: [[Dynamic Programming - Overview]], [[Dynamic Programming - Complexity]]
