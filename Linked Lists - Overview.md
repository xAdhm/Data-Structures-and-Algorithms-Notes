# Linked Lists - Overview

Requires basic object-oriented programming familiarity (classes, objects, attributes).

## The node concept
A **node** is an element with more than just one piece of data — think of an array element as conceptually having both a value and metadata (e.g. its index). Arrays store elements **contiguously in memory** (each element sits a fixed byte-offset from its neighbors), which is what enables O(1) indexing like `arr[6]`.

A **linked list** stores ordered data like an array, but is implemented using **node objects** (a custom class) rather than contiguous memory. Each node has a `next` pointer, referencing the node representing the next element in sequence.

## Example: building 1 → 2 → 3
```python
class ListNode:
    def __init__(self, val):
        self.val = val
        self.next = None

one = ListNode(1)
two = ListNode(2)
three = ListNode(3)
one.next = two
two.next = three
head = one

print(head.val)              # 1
print(head.next.val)         # 2
print(head.next.next.val)    # 3
```

## The head
The node with value `1` is called the **head** — the start of the linked list. You almost always want to keep a reference to the head, because it's the *only* node from which you can reach every other element (singly linked lists can't go backward). Losing the head reference means losing access to the rest of the list.

#dsa #algorithms #linked-lists

Related: [[Linked Lists - vs Arrays]], [[Linked Lists - Pointer Mechanics]]
