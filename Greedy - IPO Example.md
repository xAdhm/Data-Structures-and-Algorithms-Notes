# Greedy - IPO Example

## Problem: 502. IPO
`n` projects, each with a `profit[i]` and required `capital[i]`. Start with capital `w`; completing a project adds its profit to your capital. Choose up to `k` projects to maximize final capital.

## Establishing the greedy strategy
At each step, among all currently-affordable projects, always pick the one with **maximum profit**. Reasoning: picking the most profitable project directly maximizes capital gained *and* unlocks at least as many (likely more) future projects as any other affordable choice would — there's never a scenario where picking a less profitable project could unlock projects that the most profitable one wouldn't *also* unlock (since ending up with more money can never make fewer projects affordable).

This splits the problem into two sub-problems:
1. **Tracking which projects are currently affordable** as capital grows
2. **Finding the max-profit project** among the currently affordable ones, at each step

## Approach
- **Sub-problem 1:** sort projects by required capital (ascending). Use a pointer `i` tracking how far into this sorted list we've "unlocked" — every time capital grows, advance `i` past any newly-affordable projects.
- **Sub-problem 2:** exactly the [[Heaps - Overview|"repeatedly find the max"]] pattern — use a **max heap**. As projects get unlocked (pointer `i` advances), push their profits onto the heap. At each of the `k` steps, pop the heap's max and add it to `w`.

## Code
```python
import heapq

class Solution:
    def findMaximizedCapital(self, k: int, w: int, profits: List[int], capital: List[int]) -> int:
        n = len(profits)
        projects = sorted(zip(capital, profits))
        heap = []
        i = 0

        for _ in range(k):
            while i < n and projects[i][0] <= w:
                heapq.heappush(heap, -projects[i][1])
                i += 1

            if len(heap) == 0:
                # not enough money to do any more projects
                return w

            # minus because we stored negative numbers on the heap
            w -= heapq.heappop(heap)

        return w
```

`zip(capital, profits)` pairs each project's cost with its profit, and sorting this list of pairs sorts by capital (the first element of each tuple) automatically.

## Complexity
`n` = number of projects. Sorting: O(n log n). Main loop: up to `k` pop operations plus `n` total push operations across the whole run (each project pushed at most once) — heap size is bounded by `n`, so each operation is O(log n) → **O((k + n) log n) time** overall (the initial sort's O(n log n) doesn't change this bound). **Space: O(n)** for the heap.

#dsa #algorithms #greedy #heaps

Related: [[Greedy Algorithms - Overview]], [[Heaps - Overview]], [[Heaps - Top K Pattern]]
