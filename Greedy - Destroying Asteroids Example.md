# Greedy - Destroying Asteroids Example

## Problem: 2126. Destroying Asteroids
Given `asteroids` and a planet `mass`: the planet collides with asteroids one at a time, in any chosen order. If the planet's mass is less than an asteroid's, the planet is destroyed; otherwise it gains that asteroid's mass. Can all asteroids be destroyed?

## Establishing the greedy strategy
Choosing the optimal collision order: if two asteroids `x < y ≤ planet` are both currently affordable, does the order between them matter? **No** — the planet's mass only ever *increases*, so anything currently destroyable stays destroyable no matter when it's handled. There's no benefit to saving an affordable asteroid for later.

**The real question:** at each step, what's the easiest way to know which asteroids are currently affordable? **Greedily take the smallest remaining asteroid first** — if the current smallest is unaffordable, nothing else can be affordable either (everything else is even bigger), so it's immediately clear the answer is "impossible."

## Approach
Sort ascending, iterate through. At each asteroid: if it's bigger than current `mass`, return `False`. Otherwise, absorb it (`mass += asteroid`) and continue.

## Code
```python
class Solution:
    def asteroidsDestroyed(self, mass: int, asteroids: List[int]) -> bool:
        asteroids.sort()
        for asteroid in asteroids:
            if asteroid > mass:
                return False
            mass += asteroid

        return True
```

## Complexity
**O(n log n) time** — dominated by the sort (`n` = number of asteroids). **Space:** depends on the language's sort implementation — e.g. Python's Timsort uses up to O(n), while a quicksort-based language might use O(log n).

#dsa #algorithms #greedy

Related: [[Greedy Algorithms - Overview]]
