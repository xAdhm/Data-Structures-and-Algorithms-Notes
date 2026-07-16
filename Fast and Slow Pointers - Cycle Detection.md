# Fast and Slow Pointers - Cycle Detection

## Problem: 141. Linked List Cycle
Given the head of a linked list, determine if it has a cycle — some node reachable again by repeatedly following `next` pointers (i.e. a group of nodes forms a loop, and traversal never reaches `None`).

## Why "just iterate a huge number of times" doesn't work
If there's no cycle, you'd eventually hit the end. If there is one, you'd iterate forever. Picking an arbitrary large cutoff isn't a real solution — you can always construct a valid (cycle-free) linked list longer than any fixed cutoff, forcing a false positive. Hardcoding a cutoff is bad practice regardless.

## The racetrack intuition
Picture two runners on a **straight** track at different speeds — the slower one never catches the faster one; the faster one just finishes first. This is like a fast pointer reaching the end of a cycle-free list.

Now picture a **circular** track with many laps — the faster runner will eventually **lap** the slower one, meaning they'll be at the same position again at some point. This is the cycle case: a fast pointer moving 2x speed will eventually "catch up" and meet the slow pointer from behind.

**Why the fast pointer can't skip over the slow one:** once both pointers are inside the cycle, each iteration closes the gap between them by exactly one step (the fast pointer gains 2 positions per iteration, the slow pointer gains 1 — net gain of 1 per iteration). If the gap is ever 2, next iteration it's 1; if it's 1, next iteration they meet. The gap can never jump past 0 to become negative — it shrinks by exactly 1 each time, so a meeting is guaranteed if a cycle exists.

## Approach 1 (preferred): fast and slow pointers
```python
class Solution:
    def hasCycle(self, head: Optional[ListNode]) -> bool:
        slow = head
        fast = head
        while fast and fast.next:
            slow = slow.next
            fast = fast.next.next
            if slow == fast:
                return True
        return False
```
If `fast` reaches the end (`None`), there's no cycle. If `slow` and `fast` ever become the same node, a cycle exists.

**Complexity: O(n) time, O(1) space** — no extra data structure needed.

## Approach 2: hashing (for completeness — uses more space)
```python
class Solution:
    def hasCycle(self, head: Optional[ListNode]) -> bool:
        seen = set()
        while head:
            if head in seen:
                return True
            seen.add(head)
            head = head.next
        return False
```
Track every visited node in a [[Hashing - Sets|set]]. Cycle-free lists eventually hit `None`; cyclic lists eventually revisit a node already in the set.

**Complexity: O(n) time, O(n) space** — strictly worse space usage than the fast/slow approach; included here only for completeness. The fast/slow pointer solution is the better answer in an interview.

#dsa #algorithms #linked-lists #fast-slow-pointers #hashing

Related: [[Fast and Slow Pointers - Overview]], [[Hashing - Sets]]
