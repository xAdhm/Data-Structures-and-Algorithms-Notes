# Graphs - Shortest Path with Alternating Colors Example

## Problem: 1129. Shortest Path with Alternating Colors
Directed graph, `n` nodes, edges colored red or blue (given as separate `redEdges`/`blueEdges` lists). Starting at node `0`, find the shortest path to every other node such that edge colors **strictly alternate**. Return `-1` for unreachable nodes.

## Applying the state-variable idea
See [[Graphs - State Variables in BFS]]. A plain "current node" doesn't capture enough — whether the *next* edge is allowed to be red or blue depends on what color was used last. **State = `(node, color)`**, where `color` represents the color the *next* edge must be.

## Setup
- `RED = 0`, `BLUE = 1` (arbitrary — doesn't matter which is which).
- Build a **nested** hash map: `graph[color][node]` = list of neighbors reachable via an edge of that specific `color`. This extra layer lets the BFS instantly filter to only edges matching the currently-required color.
- **Toggling color:** `1 - color` flips between `0` and `1` — `f(1) = 0`, `f(0) = 1`. A clean one-liner for alternating state.

## Starting the BFS from both colors
Since the very first edge from node `0` could legally be *either* color, the 0th level of the BFS needs **two** starting states: `(0, RED)` and `(0, BLUE)` — same "0th level can hold multiple entries" idea introduced in [[Graphs - 01 Matrix Example]]'s multi-source BFS.

## Code
```python
from collections import defaultdict, deque

class Solution:
    def shortestAlternatingPaths(self, n: int, redEdges: List[List[int]], blueEdges: List[List[int]]) -> List[int]:
        RED = 0
        BLUE = 1

        graph = defaultdict(lambda: defaultdict(list))
        for x, y in redEdges:
            graph[RED][x].append(y)
        for x, y in blueEdges:
            graph[BLUE][x].append(y)

        ans = [float("inf")] * n
        queue = deque([(0, RED, 0), (0, BLUE, 0)])
        seen = {(0, RED), (0, BLUE)}

        while queue:
            node, color, steps = queue.popleft()
            ans[node] = min(ans[node], steps)

            for neighbor in graph[color][node]:
                if (neighbor, 1 - color) not in seen:
                    seen.add((neighbor, 1 - color))
                    queue.append((neighbor, 1 - color, steps + 1))

        return [x if x != float("inf") else -1 for x in ans]
```

**Why `ans[node] = min(ans[node], steps)` instead of just setting it once:** since a node can be reached via two different states (arriving via red vs. via blue), it might get dequeued twice — the `min` guards against a later, longer path accidentally overwriting an already-correct shorter answer (though in practice, thanks to BFS's ordering guarantee, the *first* visit to `ans[node]` in either color state is already the shortest — the `min` is a safety net for the dual-color entry point).

## Complexity
Since `color` only ever has 2 possible values, it doesn't change the asymptotic complexity — states are effectively still bounded by nodes × a constant. **O(n + e) time and space**, where `e` = total edges across both colors (standard [[Graphs - DFS Complexity|graph traversal bound]]), from `graph`, `seen`, and `queue`.

#dsa #algorithms #graphs #queues #hashing

Related: [[Graphs - State Variables in BFS]], [[Graphs - Shortest Path with Obstacle Elimination Example]], [[Hashing - Hash Maps]]
