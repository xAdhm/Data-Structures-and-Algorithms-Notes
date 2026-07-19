# Linked Lists - Reversing a Linked List

Reversing a linked list is a common interview problem on its own, but also frequently used as a **step** within other, larger problems (see [[Linked Lists - Reversal as Part of an Algorithm (Maximum Twin Sum)]]).

## Problem
Given `1 -> 2 -> 3 -> 4`, return `4 -> 3 -> 2 -> 1`.

## The core difficulty
In a singly linked list, once you move forward (`curr = curr.next`), you lose the ability to get back to the previous node — there's no `prev` pointer built in. To reverse direction, you need to manually track "where I came from."

## Building the solution step by step
1. At any node `curr`, we eventually need `curr.next` to point **backward**, to whatever came before it.
2. Use a `prev` pointer to track the previous node.
3. `prev` needs to update every iteration, in preparation for the next node.
4. After reversing `curr.next`, set `prev = curr`.
5. **Problem:** if we do `curr.next = prev` *before* saving the original `curr.next`, we lose our way forward into the rest of the list.
6. **Fix:** save `curr.next` in a temporary variable (`next_node`) *before* overwriting `curr.next`.

## Code
```python
def reverse_list(head):
    prev = None
    curr = head
    while curr:
        next_node = curr.next # first, make sure we don't lose the next node
        curr.next = prev      # reverse the direction of the pointer
        prev = curr           # set the current node to prev for the next node
        curr = next_node      # move on

    return prev
```

Note that the function returns `prev`, not `curr` — by the time the loop ends, `curr` is `None` (we walked off the end), while `prev` is sitting on the last real node processed — which is now the new head of the reversed list.

## Complexity
**O(n) time** (n = number of nodes; the while loop runs n times with O(1) work each), **O(1) space** (only a handful of pointers used, regardless of list length).

## General problem-solving process (applies to linked list problems broadly)
This example demonstrates the standard approach for linked list problems: figure out what you need step by step, in whatever order makes sense to *think about it* — the order you arrive at the steps mentally isn't necessarily the order they need to execute in code. Once the requirements are fully worked out, converting them to code is usually straightforward.

#dsa #algorithms #linked-lists

Related: [[Linked Lists - Pointer Mechanics]], [[Linked Lists - Swap Nodes in Pairs Example]], [[Linked Lists - Reversal as Part of an Algorithm (Maximum Twin Sum)]]
