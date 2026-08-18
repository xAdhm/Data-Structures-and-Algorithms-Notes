# Binary Search - Minimum Speed to Arrive on Time Example

## Problem: 1870. Minimum Speed to Arrive on Time
Given `hour` (float) to reach the office via `n` sequential trains, each with distance `dist[i]`, and trains only **depart on integer hours** (so you may wait between rides) — find the minimum positive integer speed for all trains, or `-1` if impossible. Answer guaranteed `≤ 10⁷` if possible.

Very similar shape to [[Binary Search - Koko Eating Bananas Example]] — same "minimum speed" framing, with the added wrinkle of integer-hour departures and an explicit "impossible" case.

## Establishing the two zones
Same reasoning as Koko: if speed `k` gets you there on time, any faster speed also works; if `k` fails, nothing slower can succeed either.

## Handling the "impossible" case up front
Since every train (except possibly the last) forces waiting until the next integer hour, each non-final train costs **at least 1 full hour**, no matter how fast you go. So if there are more trains than `hour` allows (`len(dist) > ceil(hour)`), it's impossible regardless of speed — check this **before** attempting binary search at all.

## Search space bounds
- **Minimum:** `1` (positive integer speed).
- **Maximum:** `10⁷`, given directly by the problem. **Worth noting as a general technique:** when a problem doesn't let you derive an upper bound from the input itself, just pick an arbitrarily large safe bound (e.g. `10¹⁰`) — since binary search is logarithmic, an oversized bound costs almost nothing in practice.

## The `check` function
For speed `k`: process each train's distance in order, accumulating total time `t`. Before adding each **subsequent** train's time (but not the very first), round `t` up to the next integer hour — this simulates "waiting for the next departure." The **final** train's time is **not** rounded up, since no further departure needs to be waited for.

## Code
```python
class Solution:
    def minSpeedOnTime(self, dist: List[int], hour: float) -> int:
        if len(dist) > ceil(hour):
            return -1

        def check(k):
            t = 0
            for d in dist:
                t = ceil(t)
                t += d / k

            return t <= hour

        left = 1
        right = 10 ** 7
        while left <= right:
            mid = (left + right) // 2
            if check(mid):
                right = mid - 1
            else:
                left = mid + 1

        return left
```

**Why `t = ceil(t)` before adding each distance, not after:** rounding happens at the *start* of each train ride (waiting for departure), except the very first ride (`t=0` initially, `ceil(0)=0`, so no effective rounding happens there) — this naturally handles "no rounding needed for the first train, and no rounding needed after the last one" without special-casing either end explicitly.

## Complexity
`check` costs **O(n)**, where `n = len(dist)`. Binary search runs **O(log k)** times, where `k = 10⁷` (a constant). **Technically O(n)** given the fixed bound, though it's more meaningful to describe it generally as **O(n log k)**, since `k` could vary if the bound weren't fixed by the problem. **O(1) space.**

#dsa #algorithms #binary-search

Related: [[Binary Search - Koko Eating Bananas Example]], [[Binary Search - On Solution Spaces]]
