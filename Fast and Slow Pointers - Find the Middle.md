# Fast and Slow Pointers - Find the Middle

## Problem
Given the head of a linked list with an **odd** number of nodes, return the value of the middle node.

Example: `1 -> 2 -> 3 -> 4 -> 5` → return `3`.

## Why this is tricky
The core difficulty: you don't know the length of the list up front. This rules out array-style indexing (`array[length // 2]`) unless you first convert the whole list to an array — which works, but is considered "cheating" and wouldn't be an acceptable interview solution (see [[Linked Lists - vs Arrays]] on why interviewers expect pointer manipulation, not array conversion).

## Approach 1: two-pass (find length, then find middle)
Iterate once with a dummy pointer to count the length, then iterate again from the head, moving `length // 2` steps.

```python
def get_middle(head):
    length = 0
    dummy = head
    while dummy:
        length += 1
        dummy = dummy.next

    for _ in range(length // 2):
        head = head.next

    return head.val
```

Works, but requires **two full passes** over the list.

## Approach 2 (elegant): fast and slow pointers, one pass
If one pointer moves twice as fast as the other, by the time the fast pointer reaches the end, the slow pointer — moving at half the speed — will be exactly halfway.

```python
def get_middle(head):
    slow = head
    fast = head
    while fast and fast.next:
        slow = slow.next
        fast = fast.next.next

    return slow.val
```

Only **one pass** needed — `slow` naturally lands on the middle node once the loop ends.

## Complexity
Both approaches: **O(n) time**, **O(1) space**, where `n` = number of nodes. The fast/slow version is preferred for its elegance and single-pass nature, even though both share the same asymptotic complexity.

#dsa #algorithms #linked-lists #fast-slow-pointers

Related: [[Fast and Slow Pointers - Overview]], [[Linked Lists - Dummy Pointers]]
