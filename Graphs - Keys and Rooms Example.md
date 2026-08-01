# Graphs - Keys and Rooms Example

## Problem: 841. Keys and Rooms
`n` rooms (`0` to `n-1`), all locked except room `0`. Visiting a room may reveal keys to other rooms. `rooms[i]` = keys obtainable from room `i`. Return whether all rooms can be visited.

## Recognizing the format and the question
`rooms[i]` being "a list of other rooms reachable from room `i`" is exactly an [[Graphs - Input Formats|adjacency list]] — the most convenient graph input format, since no pre-processing into a hash map is needed at all; `rooms[i]` **is** already node `i`'s neighbor list.

Rooms are nodes; keys are edges. The question "can we visit all rooms starting from room 0?" is exactly "starting a DFS from node 0, can we reach every node?"

## Approach
- Start DFS from `0`, using `seen` as usual.
- After the DFS finishes, compare `len(seen)` to `n` (the total room count, i.e. `len(rooms)`) — if they match, every room was reachable.

## Recursive code
```python
class Solution:
    def canVisitAllRooms(self, rooms: List[List[int]]) -> bool:
        def dfs(node):
            for neighbor in rooms[node]:
                if neighbor not in seen:
                    seen.add(neighbor)
                    dfs(neighbor)

        seen = {0}
        dfs(0)
        return len(seen) == len(rooms)
```

## Iterative code
```python
class Solution:
    def canVisitAllRooms(self, rooms: List[List[int]]) -> bool:
        seen = {0}
        stack = [0]

        while stack:
            node = stack.pop()
            for neighbor in rooms[node]:
                if neighbor not in seen:
                    seen.add(neighbor)
                    stack.append(neighbor)
        return len(seen) == len(rooms)
```

## Complexity
Since the input is already an adjacency list, **no pre-processing cost** is needed (contrast with [[Graphs - Number of Provinces Example]]'s adjacency-matrix conversion). **Time: O(n + e)** — standard graph DFS bound (see [[Graphs - DFS Complexity]]), each node visited once, for loops totaling `e` iterations across the whole run. **Space: O(n)** — `seen` and the recursion/stack.

#dsa #algorithms #graphs

Related: [[Graphs - Input Formats]], [[Graphs - DFS Complexity]]
