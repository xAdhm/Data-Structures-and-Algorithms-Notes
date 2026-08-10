# Heaps - Overview

A **heap** is a data structure implementing a **priority queue**. Note: "priority queue" is the abstract concept; "heap" is one specific way to implement it — but in practice the two terms are often used interchangeably (this course sticks with "heap").

## What a heap supports
- **Add an element:** O(log n)
- **Remove the minimum element:** O(log n)
- **Find the minimum element:** O(1)

A heap can instead be configured to track the **maximum** — called a **max heap** (vs. **min heap** for the minimum-tracking version). Same operations, opposite ordering.

## Why heaps are powerful
Constant-time access to the min/max, with only logarithmic-time maintenance as elements change, makes heaps extremely useful whenever you need to **repeatedly** find the max or min of a changing collection. In many problems, using a heap improves time complexity from **O(n²) to O(n log n)** — a massive improvement (for `n = 1,000,000`, that's roughly 50,000x faster).

## Implementation: binary heap (array-based)
Like [[Hashing - Hash Maps|hash maps]], every major language has a built-in heap — you generally don't need to implement one yourself, and for problem-solving purposes, only the **interface** matters. Implementation details are covered here mainly for completeness / interview trivia.

**The most common implementation: a binary heap, built on a plain array** (not node objects, unlike [[Binary Trees - Code Representation|binary trees]]).

### The structure
- Each array index represents a node in a conceptual [[Binary Trees - Overview|binary tree]].
- **Min-heap property:** if `A` is the parent of `B`, then `A.val <= B.val` — this directly guarantees the root (smallest element) is always at the very top.
- The tree must be a **complete tree** (every level full except possibly the last, filled left to right — see [[Binary Trees - BFS Overview|complete tree definition]]).

### Index math (no pointers needed)
- Root is at index `0`.
- A node at index `i` has children at indices `2i + 1` and `2i + 2`.
- This lets the tree structure be fully implicit — just arithmetic on array indices, no `left`/`right` pointers required.

### Maintaining the heap property
When elements are added or removed, the heap runs a process called **"bubbling up"** (or down) to restore the `parent.val <= child.val` property throughout the tree. This is what gives add/remove their **O(log n)** cost — proportional to the tree's height, same logarithmic reasoning as [[Binary Search Trees - Overview|BST operations]].

### Building a heap from an existing array
An existing array can be converted into a valid heap in **O(n)** (linear time) — the process itself is more involved than simple bubbling, but most languages provide a built-in method for it (see Python's `heapify` below).

## Python interface
```python
# In Python, we will use the heapq module
# Note: heapq only implements min heaps
from heapq import *

# Declaration: heapq does not give you a heap data structure.
# You just use a normal list, and heapq provides you with
# methods that can be used on this list to perform heap operations
heap = []

# Add to heap
heappush(heap, 1)
heappush(heap, 2)
heappush(heap, 3)

# Check minimum element
heap[0] # 1

# Pop minimum element
heappop(heap) # 1

# Get size
len(heap) # 2

# Bonus: convert a list to a heap in linear time
nums = [43, 2, 13, 634, 120]
heapify(nums)
# Now, you can use heappush and heappop on nums
# and nums[0] will always be the minimum element
```

## Simulating the opposite heap type
Some languages default to a min heap, others to a max heap (Python's `heapq` is min-only). **Trick for numeric values:** to simulate the opposite type, just multiply every value by `-1` before pushing, and negate again when reading — flips min-behavior into max-behavior (or vice versa) without needing a different data structure.

#dsa #algorithms #heaps

Related: [[Binary Trees - Overview]], [[Hashing - Hash Maps]], [[Binary Search Trees - Overview]]
