# Graphs - Reorder Routes Example

## Problem: 1466. Reorder Routes to Make All Paths Lead to the City Zero
`n` cities, `n - 1` directed roads (`connections[i] = [x, y]` = a road from `x` to `y`), with exactly one path between any two cities. Find the minimum number of road-direction swaps so every city can reach city `0`.

## Recognizing the structure
`n` nodes and `n - 1` edges, with exactly one path between any two nodes — this technically satisfies the definition of a **tree** (with `0` as the root), even though it's presented as a general directed graph. This shape (`n` nodes, `n-1` edges) is a common tell for tree-structured graph problems.

## The key insight
Since there's only **one** path between any two cities, the *only* way every city can reach `0` is if every road is oriented **toward** `0`. So the task reduces to: find every edge currently pointing **away** from `0`, and count them (each needs to be flipped).

## Using an undirected traversal to detect direction violations
If we DFS starting at `0` using `seen` to avoid revisiting, **every step we take is necessarily moving away from 0** (since we started there and never go back). So: at every step `node → neighbor`, if that exact directed edge `(node, neighbor)` exists in the *original* input, it must be pointing away from `0` — meaning it needs to be swapped.

**The catch:** since the actual edges are directed, a DFS respecting only the original directions might not reach every node. **Fix:** build the traversal graph as **undirected** (add both directions to the adjacency structure) purely to enable full traversal from `0` — but separately track the **original** directed edges in a set (`roads`), so direction violations can still be detected with an O(1) lookup.

## Recursive code
```python
class Solution:
    def minReorder(self, n: int, connections: List[List[int]]) -> int:
        roads = set()
        graph = defaultdict(list)
        for x, y in connections:
            graph[x].append(y)
            graph[y].append(x)
            roads.add((x, y))

        def dfs(node):
            ans = 0
            for neighbor in graph[node]:
                if neighbor not in seen:
                    if (node, neighbor) in roads:
                        ans += 1
                    seen.add(neighbor)
                    ans += dfs(neighbor)

            return ans
        seen = {0}
        return dfs(0)
```

`roads` holds only the *original* directed edges — `graph` holds both directions for traversal purposes. Checking `(node, neighbor) in roads` tells us whether the edge we just crossed matches an original "away from 0" direction.

## Iterative code
```python
class Solution:
    def minReorder(self, n: int, connections: List[List[int]]) -> int:
        roads = set()
        graph = defaultdict(list)
        for x, y in connections:
            graph[x].append(y)
            graph[y].append(x)
            roads.add((x, y))

        ans = 0
        stack = [0]
        seen = {0}
        while stack:
            node = stack.pop()
            for neighbor in graph[node]:
                if neighbor not in seen:
                    if (node, neighbor) in roads:
                        ans += 1
                    seen.add(neighbor)
                    stack.append(neighbor)

        return ans
```

## Complexity
**O(n) time and O(n) space** — the problem guarantees `n - 1` edges (= O(n)), each node visited once with constant work, and `roads`/`graph`/`seen` all bounded by O(n).

**Language note:** in C++, using `set` (as opposed to `unordered_set`) gives simpler code for storing pairs but costs O(log n) instead of O(1) per operation — trading simplicity for a small complexity hit; true O(1) is achievable with `unordered_set` if pairs are converted to an immutable hashable form.

#dsa #algorithms #graphs #hashing

Related: [[Graphs - DFS Complexity]], [[Graphs - Terminology]], [[Hashing - Sets]]
