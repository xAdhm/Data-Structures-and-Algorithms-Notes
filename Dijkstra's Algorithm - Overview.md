# Dijkstra's Algorithm - Overview

Fills in the placeholder referenced earlier in [[Code Templates - Quick Reference]].

## Weighted vs. unweighted graphs
Every graph problem covered so far used **unweighted** graphs — [[Graphs - BFS Overview|BFS]]'s "shortest path" meant the path with the **fewest edges**. A **weighted graph** assigns a value (weight) to each edge, and "shortest path" instead means the path with the **lowest total weight** (sum of edge weights along the path) — which is **not necessarily** the path with the fewest edges.

**Illustrating example:** three paths from node 0 to node 4, with edge counts vs. weights:
- Path with the fewest edges can have the **highest** total weight.
- A longer path (more edges) can have the **lowest** total weight.

As with other graph problems, expect a story wrapper — e.g. "cities connected by toll highways, find the cheapest route."

## Why BFS doesn't work here
[[Graphs - BFS Overview|BFS]] relies on unweighted graphs being equivalent to "all edge weights = 1" — its core guarantee (first visit = fewest edges) doesn't translate to "first visit = lowest total weight" once edges have varying weights. A different algorithm is needed.

## Dijkstra's algorithm
Finds the shortest (lowest-weight) path from **one source node** to **every other node** in the graph.

**Core idea:** use a **min heap** (see [[Heaps - Overview]]) to store nodes to process, ordered by the weight of the path used to reach them so far — same "store nodes to explore" role that a stack played in DFS and a queue played in BFS, just now prioritized by path weight instead of insertion order.

**Tracking best-known distances:** maintain a `distances` array (size `n`, for nodes labeled `0` to `n-1`), initialized to infinity everywhere except `distances[source] = 0`.

**At each step:** pop the node with the current minimum path weight from the heap. For each neighbor, compute `dist = curr_dist + edge_weight`:
- If `dist >= distances[neighbor]` — a shorter (or equal) path to this neighbor was already found; this path is pointless, skip it.
- If `dist < distances[neighbor]` — this is the best path to `neighbor` found so far; update `distances[neighbor] = dist` and push `(dist, neighbor)` onto the heap.

## Implementation
```python
# array of length n with large values
distances = [infinity] * n
distances[source] = 0

# min heap
heap = [(0, source)]

while heap:
    curr_dist, node = heap.pop()
    if curr_dist > distances[node]:
        # optimization step: ignore current path if we found a better one
        continue

    for nei, weight in graph[node]:  # edges from node
        dist = curr_dist + weight

        # add neighbor to heap if it creates a shorter path
        if dist < distances[nei]:
            distances[nei] = dist
            heap.push((dist, nei))
```

**Why the `curr_dist > distances[node]` check matters:** a node can be pushed onto the heap multiple times (once per improving path found to it) before it's ever popped. By the time an older, worse entry for that node gets popped, `distances[node]` may have already been improved by a better entry processed earlier — this check skips reprocessing a now-stale, suboptimal path.

## Complexity
**O((V + E) · log V) time**, where `V` = vertices, `E` = edges — heap operations cost O(log V) each, with O(V) pops and O(E) pushes overall. **Space: O(V)** for the heap and `distances`. (Doesn't include the cost of building the graph itself — see [[Graphs - Input Formats]].)

## Critical caveat: negative weight cycles break Dijkstra's
Dijkstra's algorithm **only works correctly on graphs without negative weight cycles**. If a cycle's total weight is negative, repeatedly looping through it keeps *decreasing* the path distance every pass — the algorithm will never terminate, since there's always a "better" path found by going around the cycle one more time.

See [[Dijkstra's Algorithm - Network Delay Time Example]] for a full worked application.

#dsa #algorithms #dijkstra #graphs #heaps

Related: [[Code Templates - Quick Reference]], [[Heaps - Overview]], [[Graphs - BFS Overview]], [[Dijkstra's Algorithm - Network Delay Time Example]]
