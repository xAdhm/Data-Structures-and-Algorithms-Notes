# Linked Lists - Sentinel Nodes

Terminology: the start of a linked list is the **head**, the end is the **tail**.

## The idea
**Sentinel nodes** are placeholder nodes kept at the very start and very end of a linked list, even when the list is otherwise empty. The sentinel nodes themselves are **not** considered part of the actual list content — the real head is `head.next`, and the real tail is `tail.prev`.

## Why bother
Code without sentinels is error-prone at the edges. E.g. deleting the last real node means `nextNode` would be `None`/null, and trying to access `nextNode.next` on that would crash. With a sentinel `tail`, the last real node's `next` always points to the sentinel tail instead of `None` — so edge cases at the boundaries don't need special-case handling.

Sentinels also make add/remove at the very front or back **O(1)** cleanly, since you always have guaranteed, valid pointers to reference (see [[Linked Lists - vs Arrays]] for why having a reference to the relevant position matters for O(1) operations).

## Setup
```python
class ListNode:
    def __init__(self, val):
        self.val = val
        self.next = None
        self.prev = None

head = ListNode(None)
tail = ListNode(None)
head.next = tail
tail.prev = head
```

## Operations (doubly linked list with sentinels)
```python
def add_to_end(node_to_add):
    node_to_add.next = tail
    node_to_add.prev = tail.prev
    tail.prev.next = node_to_add
    tail.prev = node_to_add

def remove_from_end():
    if head.next == tail:
        return  # list is empty

    node_to_remove = tail.prev
    node_to_remove.prev.next = tail
    tail.prev = node_to_remove.prev

def add_to_start(node_to_add):
    node_to_add.prev = head
    node_to_add.next = head.next
    head.next.prev = node_to_add
    head.next = node_to_add

def remove_from_start():
    if head.next == tail:
        return  # list is empty

    node_to_remove = head.next
    node_to_remove.next.prev = head
    head.next = node_to_remove.next
```

Both "remove" functions check `head.next == tail` first — this is exactly how sentinels let you cleanly detect an empty list (no real nodes exist between the two sentinels) without needing a separate size counter or null checks scattered throughout.

#dsa #algorithms #linked-lists

Related: [[Linked Lists - Doubly Linked List]], [[Linked Lists - Dummy Pointers]]
