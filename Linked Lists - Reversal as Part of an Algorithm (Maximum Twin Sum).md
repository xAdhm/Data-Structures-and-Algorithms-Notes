# Linked Lists - Reversal as Part of an Algorithm (Maximum Twin Sum)

Reversal isn't always the point of a problem — sometimes it's just a **tool** used along the way to a better solution. This example also reuses the [[Fast and Slow Pointers - Overview|fast and slow pointer]] technique from the previous article.

## Problem: 2130. Maximum Twin Sum of a Linked List
Given a linked list, "twin" pairs are: 1st & last node, 2nd & 2nd-last node, 3rd & 3rd-last node, etc. Return the **maximum** twin pair sum.

**Trivial solution:** convert to an array, then index pairs directly — works, but not O(1) space.

## The elegant O(1) space approach
1. **Find the middle** of the linked list using the [[Fast and Slow Pointers - Find the Middle|fast and slow pointer technique]].
2. **Reverse only the second half** of the list, starting from the middle (see [[Linked Lists - Reversing a Linked List]]).
3. After reversing the second half, each node in the first half is now exactly `n/2` positions away from its twin (`n` = total node count, found in step 1) — because the second half's order has been flipped to align with the first half's.
4. Walk the first half (`head`) and the reversed second half (starting where `slow` ended up) **simultaneously**, pointer-in-pointer, computing `first.val + second.val` at each step and tracking the max.

## Implementation
```python
def find_middle(head):
    slow = fast = head
    while fast and fast.next:
        slow = slow.next
        fast = fast.next.next
    return slow

def reverse_list(head):
    prev = None
    curr = head
    while curr:
        next_node = curr.next
        curr.next = prev
        prev = curr
        curr = next_node
    return prev

class Solution:
    def pairSum(self, head: Optional[ListNode]) -> int:
        # Step 1: find the middle of the list
        middle = find_middle(head)

        # Step 2: reverse the second half, starting at the middle
        second_half = reverse_list(middle)

        # Step 3 & 4: walk both halves together, tracking the max pair sum
        first_half = head
        ans = 0
        while second_half:
            ans = max(ans, first_half.val + second_half.val)
            first_half = first_half.next
            second_half = second_half.next

        return ans
```

**Why the loop only checks `second_half`:** the reversed second half is always the same length as (or one shorter than, for odd-length lists) the first half, so it will always run out first or at the same time — no need to check `first_half` separately.

## Complexity
- Finding the middle: O(n/2) ≈ O(n)
- Reversing the second half: O(n/2) ≈ O(n)
- Walking both halves to sum pairs: O(n/2) ≈ O(n)
- **Total time: O(n)**, **space: O(1)** — only a constant number of pointers used throughout, no array conversion needed

## Takeaway
This is a good example of combining two previously-learned techniques ([[Fast and Slow Pointers - Overview]] + [[Linked Lists - Reversing a Linked List]]) as *building blocks* inside a larger algorithm, rather than either one being the entire solution on its own.

#dsa #algorithms #linked-lists #fast-slow-pointers

Related: [[Linked Lists - Reversing a Linked List]], [[Fast and Slow Pointers - Find the Middle]]
