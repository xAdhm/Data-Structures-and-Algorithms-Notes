# Linked Lists - Doubly Linked List

A **doubly linked list** extends a singly linked list ([[Linked Lists - Singly Linked List Operations]]) by giving each node a second pointer, `prev`, referencing the previous node. This allows iteration in **both directions**.

## Why this simplifies insertion/deletion
In a singly linked list, inserting/deleting at position `i` required a reference to the node at `i - 1`, because that's the only way to reach and modify the node *before* the target. With a doubly linked list, you only need a reference to the node **at position `i` itself** — you can get to `i - 1` directly via that node's `prev` pointer.

The tradeoff: extra bookkeeping, since `prev` pointers must also be kept in sync alongside `next` pointers.

## Inserting at position i
```python
class ListNode:
    def __init__(self, val):
        self.val = val
        self.next = None
        self.prev = None

# Let node be the node at position i
def add_node(node, node_to_add):
    prev_node = node.prev
    node_to_add.next = node
    node_to_add.prev = prev_node
    prev_node.next = node_to_add
    node.prev = node_to_add
```

Four pointer updates total: the new node's `next`/`prev`, plus updating both neighbors (`prev_node.next` and `node.prev`) to point to the new node.

## Deleting the node at position i
```python
class ListNode:
    def __init__(self, val):
        self.val = val
        self.next = None
        self.prev = None

# Let node be the node at position i
def delete_node(node):
    prev_node = node.prev
    next_node = node.next
    prev_node.next = next_node
    next_node.prev = prev_node
```

Grab both neighbors first, then link them directly to each other — bypassing `node` from both directions, which fully removes it from the list (no remaining path in or out of it, since neither singly-directional pointer still leads to it).

#dsa #algorithms #linked-lists

Related: [[Linked Lists - Singly Linked List Operations]], [[Linked Lists - Sentinel Nodes]]
