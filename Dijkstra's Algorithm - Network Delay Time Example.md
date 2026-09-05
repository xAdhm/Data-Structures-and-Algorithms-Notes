# Dijkstra's Algorithm - Network Delay Time Example

## Problem: 743. Network Delay Time
`n` nodes (labeled `1` to `n`), directed weighted edges `times[i] = [u, v, w]` (signal takes `w` time from `u` to `v`). A signal starts at node `k`. Return the minimum time for **every** node to receive it, or `-1` if some node is unreachable.

## Recognizing the Dijkstra's fit
This is exactly "shortest path from one source to every other node in a weighted graph" — the precise problem [[Dijkstra's Algorithm - Overview|Dijkstra's algorithm]] solves.

## Approach
1. Build the graph as usual (see [[Graphs - Input Formats]]), attaching each edge's weight alongside its destination.
2. Run Dijkstra's from `k`.
3. The answer is the **maximum** value across the resulting `distances` array — since "every node has received the signal" only happens once the *slowest* (most distant) node finally gets it.
4. If that maximum is still the initial "infinity" placeholder, some node was never reached at all → return `-1`.

**Indexing note:** nodes are given **1-indexed**; subtract 1 from every node label when building the graph to work with standard 0-indexed arrays.

## Code
```python
class Solution:
    def networkDelayTime(self, times: List[List[int]], n: int, k: int) -> int:
        graph = defaultdict(list)
        for x, y, z in times:
            graph[x - 1].append([y - 1, z])

        distances = [inf] * n
        distances[k - 1] = 0
        heap = [(0, k - 1)]
        while heap:
            curr_dist, node = heappop(heap)
            if curr_dist > distances[node]:
                continue

            for nei, weight in graph[node]:
                dist = curr_dist + weight
                if dist < distances[nei]:
                    distances[nei] = dist
                    heappush(heap, (dist, nei))
        ans = max(distances)
        return ans if ans < inf else -1
```

This is close to a direct copy of the [[Dijkstra's Algorithm - Overview|general Dijkstra's template]] — the only real additions are the graph-building step and the final "take the max, check for infinity" logic specific to this problem's question.

## Complexity
**O((V + E) log V) time**, where `V = n`, `E = len(times)` — standard Dijkstra's bound (see [[Dijkstra's Algorithm - Overview]]). **Space: O(V)** for `distances` and the heap, plus O(E) for the built graph.

#dsa #algorithms #dijkstra #graphs

Related: [[Dijkstra's Algorithm - Overview]], [[Graphs - Input Formats]]
