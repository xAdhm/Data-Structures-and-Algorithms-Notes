# Graphs - Open the Lock Example

## Problem: 752. Open the Lock
A 4-wheel lock (digits 0-9 each, wrapping), starting at `"0000"`. One move = turn one wheel by one slot. Given blocked codes `deadends` (the lock can't land on these), return the minimum moves to reach `target`.

## Recognizing the implicit graph
Per [[Graphs - Implicit Graphs]]: the problem involves transitioning between **states** (lock readings), and asks for the **minimum number of moves** — both strong signals for a graph + [[Graphs - BFS Overview|BFS]] approach, despite the input looking nothing like a standard graph format.

**Nodes:** every possible 4-digit lock state (`"0000"` through `"9999"`).
**Edges:** two states are neighbors if they differ in exactly **one** wheel position by exactly `1` (accounting for wrap-around: `9 ↔ 0`).

## Generating neighbors
For each of the 4 positions, try both `-1` and `+1` (mod 10, to handle wrap-around) — this produces up to 8 neighbor states per node.

## Handling deadends
Since we can never land on a `deadends` code, simply **pre-load `seen` with all deadend codes** before starting BFS — `seen` already exists to prevent revisits, so this reuses that exact mechanism to also enforce "never visit this state at all." Cleaner than adding a separate `if neighbor in deadends` check everywhere.

**Edge case:** if `"0000"` itself is a deadend, return `-1` immediately (can't even start).

## Code
```python
class Solution:
    def openLock(self, deadends: List[str], target: str) -> int:
        def neighbors(node):
            ans = []
            for i in range(4):
                num = int(node[i])
                for change in [-1, 1]:
                    x = (num + change) % 10
                    ans.append(node[:i] + str(x) + node[i + 1:])

            return ans
        if "0000" in deadends:
            return -1

        queue = deque([("0000", 0)])
        seen = set(deadends)
        seen.add("0000")

        while queue:
            node, steps = queue.popleft()
            if node == target:
                return steps

            for neighbor in neighbors(node):
                if neighbor not in seen:
                    seen.add(neighbor)
                    queue.append((neighbor, steps + 1))

        return -1
```

This is otherwise a completely standard [[Graphs - BFS Overview|BFS]] template — the only "trick" is recognizing that lock states form an implicit graph in the first place.

## Complexity
For this specific problem (fixed at 4 wheels, 10 digits): **O(d) time**, where `d = len(deadends)`, since converting `deadends` to a set dominates — everything else is bounded by constants (10⁴ possible states max).

**General case (n wheels instead of 4):** there are `10ⁿ` possible states. At each state, generating neighbors costs O(n²) — looping over `n` wheels while doing O(n) string concatenation per neighbor (since strings are immutable — see [[String Building - O(n) Technique]]). This gives **O(10ⁿ·n² + d)** overall. With mutable strings (e.g. C++), this drops to **O(10ⁿ·n + d)**.

#dsa #algorithms #graphs #queues

Related: [[Graphs - Implicit Graphs]], [[Graphs - BFS Overview]], [[String Building - O(n) Technique]]
