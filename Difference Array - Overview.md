# Difference Array - Overview

Not super common, but valuable to know cold — hard to derive on the spot in an interview if you haven't seen it before.

## When to use it
Problems involving **intervals of events** along a number line (representing time, position, etc.), where each event has a start and end point and a value associated with it while active. Input typically arrives as a 2D array of `[left, right, value]` (or an equivalent form), with a story along the lines of "between `left` and `right`, there is `value` of something."

## The core technique
Instead of directly marking every position an event covers (expensive if intervals are long), just record the **change** at the two boundary points:
- At `left`: `arr[left] += value` (the effect "starts" here)
- At `right`: `arr[right] -= value` (the effect "ends" here)

After processing every event this way, running a [[Prefix Sum - Overview|prefix sum]] over `arr` reconstructs the actual value at every position — because the running sum naturally "picks up" a value at its start and "drops" it at its end.

## Worked example: 1094. Car Pooling
A car with `capacity` seats; `trips[i] = [numPassengers, from, to]` — picks up `numPassengers` at `from`, drops them at `to`. Can all trips be completed without ever exceeding `capacity`?

**Mapping to the pattern:** the "number line" is the road; each trip is an event; `from` = left, `to` = right, `numPassengers` = value.

**Approach:**
1. Find `farthest = max(to)` across all trips, and build `arr` of length `farthest + 1`.
2. For each trip: `arr[from] += numPassengers`, `arr[to] -= numPassengers`.
3. Run a prefix sum over `arr` — at each position, the running sum is the current passenger count. If it ever exceeds `capacity`, return `False`.

```python
class Solution:
    def carPooling(self, trips: List[List[int]], capacity: int) -> bool:
        arr = [0] * (max(trip[2] for trip in trips) + 1)
        for (value, left, right) in trips:
            arr[left] += value
            arr[right] -= value
        curr = 0
        for i in range(len(arr)):
            curr += arr[i]
            if curr > capacity:
                return False

        return True
```

## Complexity
**O(n + m) time and space**, where `n` = number of trips, `m` = the farthest `to` value. Without this technique, the alternative would require sorting trips first — **O(n log n)**.

See [[Difference Array - Sparse Coordinates Variant]] for the "equivalent form" case, where positions are too large/sparse to build a literal array.

#dsa #algorithms #prefix-sum #difference-array

Related: [[Prefix Sum - Overview]], [[Difference Array - Sparse Coordinates Variant]]
