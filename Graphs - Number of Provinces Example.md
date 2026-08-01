# Graphs - Number of Provinces Example

## Problem: 547. Number of Provinces
Given an `n x n` matrix `isConnected` (an [[Graphs - Input Formats|adjacency matrix]]) where `isConnected[i][j] = 1` means cities `i` and `j` are directly connected, return the number of provinces — groups of directly/indirectly connected cities with no connections to cities outside the group.

## Recognizing the pattern
This is an **undirected** graph (given `isConnected[i][j] = isConnected[j][i]`), and "number of provinces" = number of [[Graphs - Terminology|connected components]]. Each city is a node; each province is a connected component.

## Key property: DFS from any node visits its entire connected component
In an undirected graph, starting a traversal from any node will visit **every** node in that node's connected component — same idea as how a tree traversal starting at the root visits every node in the tree.

## Approach
1. **Pre-process** the adjacency matrix into a hash map (`node → neighbor list`), per [[Graphs - Input Formats]].
2. Maintain a `seen` set (see [[Graphs - DFS Implementation Differences from Trees]]) to avoid cycles and redundant visits.
3. Iterate `i` from `0` to `n-1`. Whenever `i` isn't in `seen`, it means we've found a **new, unvisited** province — increment the answer and run DFS from `i`, marking every node in that entire component as seen along the way.
4. Because DFS from `i` marks the *whole* component as visited, later iterations of `i` will skip over every node already covered — guaranteeing each province is only counted once.

## Recursive code
```python
from collections import defaultdict

class Solution:
    def findCircleNum(self, isConnected: List[List[int]]) -> int:
        def dfs(node):
            for neighbor in graph[node]:
                # the next 2 lines are needed to prevent cycles
                if neighbor not in seen:
                    seen.add(neighbor)
                    dfs(neighbor)

        # build the graph
        n = len(isConnected)
        graph = defaultdict(list)
        for i in range(n):
            for j in range(i + 1, n):
                if isConnected[i][j]:
                    graph[i].append(j)
                    graph[j].append(i)

        seen = set()
        ans = 0

        for i in range(n):
            if i not in seen:
                # add all nodes of a connected component to the set
                ans += 1
                seen.add(i)
                dfs(i)

        return ans
```

## Iterative DFS helper
```python
def dfs(start):
    stack = [start]
    while stack:
        node = stack.pop()
        for neighbor in graph[node]:
            if neighbor not in seen:
                seen.add(neighbor)
                stack.append(neighbor)
```

## Complexity
Technically **O(n²) time** here specifically, because the input is an adjacency matrix — building the graph requires scanning the full matrix regardless of how many actual edges exist (see [[Graphs - DFS Complexity]]). The general `O(n + e)` traversal cost is dominated by this O(n²) build step. **Space: O(n + e)** — same reasoning as [[Graphs - DFS Complexity]].

#dsa #algorithms #graphs #hash-map

Related: [[Graphs - DFS Complexity]], [[Graphs - Terminology]], [[Graphs - Number of Islands Example]]
