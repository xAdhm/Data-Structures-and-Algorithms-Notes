# Graphs - Evaluate Division Example

## Problem: 399. Evaluate Division
Given `equations[i] = [x, y]` and `values[i]`, meaning `x / y = values[i]`, and a list of `queries[i] = [a, b]` asking for `a / b` — return the answer to each query, or `-1` if it can't be determined.

Example: `equations = [["a","b"],["b","c"]]`, `values = [2, 3]` (meaning `a/b=2`, `b/c=3`) → query `["a","c"]` → answer `6` (derivable: `a/c = (a/b)·(b/c) = 2·3 = 6`).

## Recognizing the implicit graph
Per [[Graphs - Implicit Graphs]] — this doesn't look like a graph at all on the surface, but: treat each **variable** (`a`, `b`, `c`, ...) as a **node**. Each equation `x/y = val` becomes an **edge** from `x` to `y`.

## New concept: weighted edges
Every graph example so far has been **unweighted** — edges just represented "connected" with no associated value. Weighted graphs (edges carrying a numeric value) generally require more advanced algorithms and are usually out of scope for typical interviews — but this problem is a case where a weighted-graph *idea* shows up in a form still solvable with plain DFS/BFS.

**The weight here is the ratio.** If `a/b = 5`, the edge `a → b` carries weight `5` — meaning "a is 5 times b." Traversing multiple edges **multiplies** their weights together: if `a/b = 5` and `b/c = 2`, walking `a → b → c` gives `5 × 2 = 10`, which is exactly `a/c`.

## Building the graph
Use a nested hash map: `graph[x][y] = val` represents the edge `x → y` with weight `val`.

**Critical detail — edges are undirected (in a specific weighted sense):** if `x/y = val`, then necessarily `y/x = 1/val` too. Both directions must be added when building the graph, each with its own (reciprocal) weight.

## Answering a query
For query `(start, end)`: traverse from `start`, carrying along a running `ratio` (starting at `1`). Each time you cross an edge to a neighbor, multiply `ratio` by that edge's weight. If you reach `end`, `ratio` is the answer. If `start` isn't even in the graph, or `end` is never reached, return `-1`.

## Code
```python
from collections import defaultdict

class Solution:
    def calcEquation(self, equations: List[List[str]], values: List[float], queries: List[List[str]]) -> List[float]:
        def answer_query(start, end):
            # no info on this node
            if start not in graph:
                return -1

            seen = {start}
            stack = [(start, 1)]

            while stack:
                node, ratio = stack.pop()
                if node == end:
                    return ratio

                for neighbor in graph[node]:
                    if neighbor not in seen:
                        seen.add(neighbor)
                        stack.append((neighbor, ratio * graph[node][neighbor]))
            return -1

        graph = defaultdict(dict)
        for i in range(len(equations)):
            numerator, denominator = equations[i]
            val = values[i]
            graph[numerator][denominator] = val
            graph[denominator][numerator] = 1 / val

        ans = []
        for numerator, denominator in queries:
            ans.append(answer_query(numerator, denominator))

        return ans
```

**Note:** `answer_query` is implemented iteratively with a stack (DFS), but — as usual — either DFS or BFS works fine here, since the problem doesn't require *shortest* path, just *any* valid path (there's only ever one path between two connected variables anyway, given the graph's structure).

## Complexity
Let `n` = number of distinct variables (bounded by `equations.length`), `e` = number of edges (`2 × equations.length`, since each equation adds both directions), `q` = number of queries.

Each query triggers a full graph traversal costing `O(n + e)` (standard [[Graphs - DFS Complexity|graph traversal bound]]). With `q` queries: **O(q · (n + e)) time**. **Space: O(n + e)** for `graph`, `seen`, and the stack (not counting the output array).

#dsa #algorithms #graphs #hashing

Related: [[Graphs - Implicit Graphs]], [[Graphs - DFS Complexity]], [[Hashing - Hash Maps]]
