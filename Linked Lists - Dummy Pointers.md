# Linked Lists - Dummy Pointers

You generally want to preserve a reference to the actual **head** of a linked list at all times (see [[Linked Lists - Overview]]) — losing it means losing access to the rest of the list, since a singly linked list can't be traversed backward.

## The problem
If you traverse using the `head` variable directly (e.g. `head = head.next` in a loop), you destroy the original head reference by the time traversal finishes.

## The fix: traverse with a separate "dummy" pointer
Instead of moving `head` itself, assign a second variable to the same starting node and move *that* one instead — leaving `head` untouched.

```python
def get_sum(head):
    ans = 0
    dummy = head
    while dummy:
        ans += dummy.val
        dummy = dummy.next

    # same result as before, but we still have a pointer at the head
    return ans
```

This relies directly on the assignment behavior covered in [[Linked Lists - Pointer Mechanics]]: `dummy = head` makes `dummy` point to the same node as `head`, but reassigning `dummy` afterward (`dummy = dummy.next`) has no effect on what `head` points to.

## Practical takeaway
Whenever a function receives `head` as a parameter and needs to traverse/modify the list, prefer creating a separate traversal pointer (commonly named `dummy`, `curr`, or `ptr`) rather than reassigning `head` directly — this preserves the original reference for later use (e.g. returning `head` at the end of the function, or referencing it again after the loop).

#dsa #algorithms #linked-lists

Related: [[Linked Lists - Pointer Mechanics]], [[Linked Lists - Overview]]
