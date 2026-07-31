# Graphs - DFS Implementation Differences from Trees

## No obvious starting point
A binary tree always has a `root` to start from. A graph doesn't necessarily have an obvious "start" — which node to begin traversal from depends entirely on the specific problem.

## Neighbor access: pointers vs. iteration
- **Trees:** each node directly references `node.left`/`node.right` — fixed, named pointers.
- **Graphs:** a node can have any number of neighbors, so accessing them requires a `for` loop over whatever structure holds them (see [[Graphs - Input Formats]] — usually a pre-built hash map).

## DFS structure is otherwise the same
Recursive graph DFS follows the identical shape as [[Binary Trees - DFS Overview|tree DFS]]: check the base case, recursively call on all neighbors (instead of just two fixed children), do the problem's logic, return the answer. Iterative implementation with an explicit [[Stacks - Overview|stack]] also still works, same as [[Binary Trees - Iterative DFS|iterative tree DFS]].

## The critical new problem: cycles
Tree DFS never worried about infinite loops — edges only moved "downward" from parent to child, so once you left a node, there was no path back to it (same reason [[Binary Trees - Terminology|trees are always acyclic]]).

**Graphs don't have this guarantee.** Any undirected graph, or any directed graph containing a cycle, can cause naive tree-style DFS to loop **forever** — e.g. a relationship like `A <-> B` lets you bounce between the two indefinitely. This is the same cycle danger covered in [[Fast and Slow Pointers - Cycle Detection]] for linked lists.

## The fix: a `seen` set
Since most graph problems only need (and want) to visit each node once:
- Maintain a `seen` set.
- Before visiting a node, check if it's already in `seen`.
- If not, add it to `seen`, *then* visit it.

Since [[Hashing - Sets|set]] add/check operations are O(1), this keeps each node visited exactly once, in constant time per check — preventing both infinite loops and redundant revisits.

**Language note:** Python's set-based `seen` is simple and fast. In languages like C++, an array can be faster in practice when the range of possible node values is known upfront (common in graph problems, since nodes are frequently labeled `0` to `n-1`) — either approach gives the same time complexity, it's purely an implementation detail.

#dsa #algorithms #graphs #stacks #hashing

Related: [[Graphs - Overview]], [[Binary Trees - DFS Overview]], [[Fast and Slow Pointers - Cycle Detection]], [[Hashing - Sets]]
