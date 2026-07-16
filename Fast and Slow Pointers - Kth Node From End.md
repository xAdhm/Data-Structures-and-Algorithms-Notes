# Fast and Slow Pointers - Kth Node From End

## Problem
Given the head of a linked list and integer `k`, return the `k`th node from the end.

Example: `1 -> 2 -> 3 -> 4 -> 5`, `k = 2` → return the node with value `4` (2nd from the end).

Similar in spirit to [[Fast and Slow Pointers - Find the Middle]] — array conversion or a two-pass length-then-seek approach would both work, but there's a more elegant one-pass solution.

## Approach: maintain a fixed gap of k between two pointers
1. Advance `fast` by `k` steps first, so it's exactly `k` nodes ahead of `slow`
2. Then advance both pointers together, one step at a time, until `fast` reaches the end (`None`)
3. Since the gap between them stays fixed at `k` the whole time, when `fast` runs out, `slow` is necessarily sitting exactly `k` nodes behind the end — the answer

```python
def find_node(head, k):
    slow = head
    fast = head
    for _ in range(k):
        fast = fast.next

    while fast:
        slow = slow.next
        fast = fast.next

    return slow
```

## Complexity
**O(n) time, O(1) space**, where `n` = number of nodes — same reasoning as [[Fast and Slow Pointers - Find the Middle]]: single pass, no extra data structures.

#dsa #algorithms #linked-lists #fast-slow-pointers

Related: [[Fast and Slow Pointers - Overview]], [[Fast and Slow Pointers - Find the Middle]]
