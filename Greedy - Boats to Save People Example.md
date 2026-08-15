# Greedy - Boats to Save People Example

## Problem: 881. Boats to Save People
Given `people` (weights) and a `limit`: each boat holds at most 2 people, combined weight ≤ `limit`. Find the minimum number of boats needed (no person exceeds `limit` alone).

## Establishing the greedy strategy
Minimizing boats means maximizing how often a boat carries **2** people instead of 1. At any moment, let `x` = heaviest remaining person, `y` = lightest remaining person:
- **If `x + y > limit`:** `x` can't pair with *anyone* — `y` is already the lightest possible partner, and it doesn't fit. `x` must go alone.
- **If `x + y ≤ limit`:** `y` (the lightest) could pair with *anyone*, since `x` is the heaviest possible partner and it still fits. To make the most of the boat, pair `y` with the **heaviest** possible person (`x`) — this uses the boat's capacity most efficiently and simplifies the remaining problem (no longer need to worry about placing `x`).

Every valid pairing reduces the answer by exactly 1 regardless of who's paired — so there's no downside to greedily trying to pair the extremes together whenever possible; it can only help future pairings by resolving the heaviest person as early as possible. (As with the other examples, not a formal proof, but a sufficient interview-level explanation — see [[Greedy Algorithms - Overview]].)

## Approach
Sort ascending, use [[Two Pointers - Converging Pointers Method|two pointers]] converging from both ends: `i` = lightest, `j` = heaviest.
- Each iteration: `j` (heaviest remaining) always takes a boat. If `people[i] + people[j] <= limit`, `i` (lightest) joins them too.
- `j` always decrements each iteration (heaviest person is always resolved); `i` only increments when it successfully pairs.

## Code
```python
class Solution:
    def numRescueBoats(self, people: List[int], limit: int) -> int:
        ans = 0
        i = 0
        j = len(people) - 1
        people.sort()

        while i <= j:
            if people[i] + people[j] <= limit:
                i += 1
            j -= 1
            ans += 1

        return ans
```

## Complexity
The two-pointer sweep itself is O(n), but sorting dominates: **O(n log n) time**, where `n = len(people)`. **Space:** depends on the sort implementation, same caveat as the other examples in this chapter.

#dsa #algorithms #greedy

Related: [[Greedy Algorithms - Overview]], [[Two Pointers - Converging Pointers Method]]
