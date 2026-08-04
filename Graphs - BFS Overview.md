# Graphs - BFS Overview

Like with trees, in many graph problems it doesn't matter whether you use [[Graphs - DFS Complexity|DFS]] or BFS — people usually default to DFS since it's faster/cleaner to implement, especially recursively. Every example in the [[Graphs - DFS Complexity|DFS chapter]] could also be solved with BFS.

## When BFS is clearly better: shortest path problems
In trees, BFS shined for level-based problems (see [[Binary Trees - BFS vs DFS]]). In graphs, BFS shines almost exclusively when you need the **shortest path**.

## The key guarantee
BFS on a graph visits nodes according to their **distance from the starting point** — same idea as [[Binary Trees - BFS Overview|tree BFS visiting nodes level by level]]. Treat the starting node as a conceptual "root": its neighbors are the next level, their neighbors are the level after, and so on — even though most graphs aren't tree-shaped.

**The core BFS property:** every time you visit a node for the first time, you're guaranteed to have reached it in the **minimum possible number of steps** from the start.

## Why this mattered less for trees
In a binary tree, this guarantee was automatic even with DFS, because there's only **one possible path** from the root to any node (tree structure forbids multiple paths). In a general graph, there can be **many** different paths between two nodes — BFS is what guarantees you find the *shortest* one, out of however many exist.

## Implementation: queue instead of stack
DFS was implemented primarily via recursion (a stack under the hood). BFS uses an explicit [[Queues - Overview|queue]], iteratively — same as [[Binary Trees - BFS Overview|binary tree BFS]].

## For loop or not?
With tree BFS, a `for` loop inside the `while` loop let us process each level as a distinct group (useful for "max value per level," etc. — see [[Binary Trees - Largest Value in Each Row Example]]). For **shortest path** problems, we usually don't care about levels as a group — we just want to know when we've *reached* a specific target. Two equally valid approaches:
1. **Associate a step count with each node** directly in the queue (e.g. `(node, steps)` tuples) — no `for` loop needed, just check `steps` whenever the target is dequeued.
2. **Keep the level-based `for` loop format**, incrementing a `level` counter once per `while` iteration, and return `level` when the target is found.

## Worked examples
- [[Graphs - Shortest Path in Binary Matrix Example]] — the foundational shortest-path-in-a-grid pattern
- [[Graphs - All Nodes Distance K in Binary Tree Example]] — converting a tree into an undirected graph to enable BFS beyond parent-only pointers
- [[Graphs - 01 Matrix Example]] — multi-source BFS (starting from *many* nodes at once)
- [[Graphs - State Variables in BFS]] — extending "node" into richer states (obstacle removals, edge colors) for more complex shortest-path variants

#dsa #algorithms #graphs #queues

Related: [[Graphs - DFS Complexity]], [[Binary Trees - BFS Overview]], [[Queues - Overview]]
