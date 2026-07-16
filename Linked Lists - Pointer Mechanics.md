# Linked Lists - Pointer Mechanics

Understanding pointer manipulation is essential both for linked list problems specifically, and as a fundamental software engineering skill generally.

## Assignment (`=`)
When you assign a pointer to an existing node, the pointer refers to that object in memory. Languages like C++ have explicit pointers (`*`); in languages without explicit pointer syntax (Python, Java, etc.), all non-primitive variables (custom class objects) behave as pointers/references anyway.

```python
ptr = head
head = head.next
head = None
```

**Key concept:** `ptr` still refers to the *original* head node even after `head` is reassigned or set to `None`. Variables keep pointing to whatever node they were assigned, unless *that specific variable* is directly reassigned (`ptr = something` is the only way to change what `ptr` points to — reassigning `head` doesn't affect `ptr`).

## Chaining `.next`
`head.next.next` — everything before the *final* `.next` refers to a single node. E.g. given `1 -> 2 -> 3` with `head` at node `1`: `head.next` is node `2`, so `head.next.next` means "`.next` of node 2," which is node `3`. This chaining is a frequently useful technique for reaching nodes without intermediate variables.

## Traversal — iterative
```python
def get_sum(head):
    ans = 0
    while head:
        ans += head.val
        head = head.next

    return ans
```
The final node's `next` is `None` (null) — so after `head = head.next` on the last node, `head` becomes `None` and the loop ends. Moving to `head.next` each iteration is the linked-list equivalent of incrementing an index when iterating over an array.

## Traversal — recursive
```python
def get_sum(head):
    if not head:
        return 0

    return head.val + get_sum(head.next)
```
Base case: an empty list (`head` is `None`) contributes `0`. Otherwise, the current node's value plus the sum of everything after it.

#dsa #algorithms #linked-lists

Related: [[Linked Lists - Overview]], [[Recursion - Base Cases]], [[Linked Lists - Singly Linked List Operations]]
