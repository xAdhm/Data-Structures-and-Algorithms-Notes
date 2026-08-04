# Graphs - DFS Complexity

## Why graph DFS complexity differs from tree DFS
With [[Binary Trees - DFS Overview|binary tree DFS]], each node visit was O(1) work, because a node has at most 2 children — no loop needed, just reference `node.left`/`node.right` directly.

With [[Graphs - DFS Implementation Differences from Trees|graph DFS]], a node can have **any number** of neighbors, so visiting a node requires a `for` loop over its neighbor list — not constant work.

## Time complexity: O(n + e)
- Each node is visited **at most once** (enforced by the `seen` set).
- A node's edges are only iterated over when that node is being visited.
- Since each node is visited once, its edges are iterated over exactly once too.
- Therefore, **all edges across the entire algorithm are processed exactly once total** → O(e)
- Combined with visiting all nodes once → **O(n + e)**, where `n` = number of nodes, `e` = number of edges.

This is the same amortized-analysis shape as [[Sliding Window - Why It's Efficient|the sliding window nested-loop argument]]: an inner loop that looks expensive per-outer-iteration is actually bounded in total across the *whole* algorithm, not per node.

**Worst case:** if every node connects to every other node, `e = n²`.

## Special case: adjacency matrix input
If the graph is given as an [[Graphs - Input Formats|adjacency matrix]], building the neighbor hash map requires scanning the full `n × n` matrix regardless of how many edges actually exist — so building the graph alone costs **O(n²)**. Since `e ≤ n²` always, the `O(e)` traversal term is dominated by this O(n²) build cost and can be dropped from the final time complexity in that specific case.

## Space complexity: O(n + e)
- Storing the built graph (edges as adjacency lists): space grows with the number of edges actually stored, **not** with `n²` — even for an adjacency matrix input, the hash map itself only grows based on edges that genuinely exist.
- `seen` set: up to O(n)
- Recursion call stack (or explicit stack, iteratively): up to O(n) in the worst case

Total: **O(n + e)**. This is *not* O(n²) even when built from an adjacency matrix — time and space complexity differ here because building the graph always scans the full matrix (time cost), but only stores what actually exists (space cost).

#dsa #algorithms #graphs #big-o

Related: [[Graphs - DFS Implementation Differences from Trees]], [[Sliding Window - Why It's Efficient]]
