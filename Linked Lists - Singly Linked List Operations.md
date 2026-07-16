# Linked Lists - Singly Linked List Operations

A **singly linked list** is the standard type: each node only points to the *next* node (via a `next` pointer) — no way to move backward.

## Inserting at position i
To insert a new node so it becomes the element at position `i`, you need a pointer to the node currently at position **i - 1**. Call the node currently at position `i` (before insertion) `x`. After insertion:
- The new node's `next` should point to `x` (the new node "takes over" position i, pushing x to i+1)
- The node at `i - 1`'s `next` should point to the new node

```python
class ListNode:
    def __init__(self, val):
        self.val = val
        self.next = None

# Let prev_node be the node at position i - 1
def add_node(prev_node, node_to_add):
    node_to_add.next = prev_node.next
    prev_node.next = node_to_add
```

**Order matters:** set `node_to_add.next` *before* overwriting `prev_node.next` — otherwise you'd lose the reference to the rest of the list.

## Deleting the node at position i
Again requires a pointer to the node at position **i - 1**. The node at `i + 1` (call it `x`) needs to become the new `i`-th node — so `prev_node.next` should point directly to `x`, skipping over the node being deleted.

```python
class ListNode:
    def __init__(self, val):
        self.val = val
        self.next = None

# Let prev_node be the node at position i - 1
def delete_node(prev_node):
    prev_node.next = prev_node.next.next
```

`prev_node.next` is the node being deleted; `prev_node.next.next` is the node after it, which should be kept. Overwriting `prev_node.next` to skip directly to that node severs the only path to the deleted node — since nothing else in a singly linked list can point *backward* to it, it's effectively removed from the list even though it still technically exists in memory.

## Complexity
- **O(1)** if you already have a reference to the node at `i - 1`
- **O(n)** if you don't, since you'd need to iterate from the head to find it first

In practice, you typically won't manually seek out position `i - 1` before doing an operation — most problems perform these operations *while already iterating* through the list, meaning you naturally have the needed pointer at hand.

#dsa #algorithms #linked-lists

Related: [[Linked Lists - Pointer Mechanics]], [[Linked Lists - Doubly Linked List]]
