# Dynamic Programming - Complexity

Complexity analysis for [[Dynamic Programming - Overview|DP]] follows the exact same logic used for [[Graphs - DFS Complexity|graph and tree traversal]]: since each **state** is computed only once (thanks to memoization), if there are `N` possible states and each costs `F` work to compute, total time is **O(N · F)**.

## Space complexity
**O(N)** — top-down: the memoization hash map ends up holding every computed state. Bottom-up: the tabulation array is sized to match the number of states. (In many problems, bottom-up implementations can have their space complexity **improved** further — top-down generally can't be optimized the same way. Covered later in the chapter.)

## Calculating N (the number of states)
`N` = the **cardinality** of the state variables — i.e., multiply together the range of possible values for each [[Dynamic Programming - State|state variable]].

**Example:** a problem with three state variables — `i` (iterating over `nums`), `k` (given by the problem), and `holding` (boolean) — has `N = nums.length * k * 2` total states. If each state costs O(1) to compute, overall time and space complexity is **O(n · k)**, where `n = nums.length`.

#dsa #algorithms #dynamic-programming #big-o

Related: [[Dynamic Programming - State]], [[Dynamic Programming - Overview]], [[Graphs - DFS Complexity]]
