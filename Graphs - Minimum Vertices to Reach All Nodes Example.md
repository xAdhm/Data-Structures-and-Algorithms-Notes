# Graphs - Minimum Vertices to Reach All Nodes Example

## Problem: 1557. Minimum Number of Vertices to Reach All Nodes
Given a **directed acyclic graph** (DAG) with `n` vertices and a directed edge array, find the smallest set of vertices from which all nodes are reachable.

Notably, **this problem doesn't require DFS at all** — included as an exercise in graph mechanics rather than traversal.

## Reframing the question
"Smallest set of nodes from which all others are reachable" is equivalent to: "the set of nodes that **cannot** be reached from any other node." Reasoning: if some node *can* be reached from another node, it'd be redundant to include it directly — including its "parent" instead already covers it.

## Connecting to indegree
A node can't be reached from any other node exactly when it has **[[Graphs - Terminology|indegree]] 0** — no edges enter it at all. So the answer is simply: every node whose indegree is `0`.

## Code
```python
class Solution:
    def findSmallestSetOfVertices(self, n: int, edges: List[List[int]]) -> List[int]:
        indegree = [0] * n
        for _, y in edges:
            indegree[y] += 1

        return [node for node in range(n) if indegree[node] == 0]
```

## Why the DAG (acyclic) guarantee matters
If cycles were allowed, this approach could fail. E.g. a graph that's just one big cycle (a circle): every node has indegree ≥ 1 (each is reached by the node before it in the cycle), so **no** node would have indegree 0 — the algorithm would return an empty set, even though *some* single node in the cycle should technically be a valid answer (any one of them can reach all the others by going around). The problem statement guarantees the graph is acyclic, so this edge case never actually arises here.

## Complexity
**O(n + e) time** — one pass over all edges to build `indegree`, one pass over all nodes to filter. **O(n) space** for the `indegree` array.

#dsa #algorithms #graphs

Related: [[Graphs - Terminology]], [[Graphs - DFS Complexity]]
