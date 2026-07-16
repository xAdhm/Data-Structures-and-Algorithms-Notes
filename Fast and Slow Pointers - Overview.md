# Fast and Slow Pointers - Overview

Fast and slow pointers is a specific implementation of the [[Two Pointers - Overview|two pointers]] technique — but instead of pointers moving in lockstep, they move **differently**: at different speeds, from different starting locations, or some other abstract distinction.

## The classic shape: fast moves 2x speed
Usually, the "fast" pointer advances two nodes per iteration, while the "slow" pointer advances one node per iteration (not a strict requirement, just the common case).

```python
# head is the head node of a linked list
def fn(head):
    slow = head
    fast = head

    while fast and fast.next:
        # Do something here
        slow = slow.next
        fast = fast.next.next
```

**Why check `fast.next` too, not just `fast`:** if `fast` is at the final node, `fast.next` is `None` — trying to then access `fast.next.next` would error (calling `.next` on `None`). Checking both conditions prevents that.

## Common applications
- Finding the middle of a linked list — see [[Fast and Slow Pointers - Find the Middle]]
- Detecting a cycle — see [[Fast and Slow Pointers - Cycle Detection]]
- Finding the kth node from the end — see [[Fast and Slow Pointers - Kth Node From End]]

#dsa #algorithms #linked-lists #two-pointers #fast-slow-pointers

Related: [[Two Pointers - Overview]], [[Linked Lists - Overview]]
