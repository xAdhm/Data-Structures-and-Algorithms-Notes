# Linked Lists - Swap Nodes in Pairs Example

## Problem: 24. Swap Nodes in Pairs
Given the head of a linked list, swap every adjacent pair of nodes.

Example: `1 -> 2 -> 3 -> 4 -> 5 -> 6` → `2 -> 1 -> 4 -> 3 -> 6 -> 5`

## Working out the requirements, one pair at a time
Consider the current pair `A -> B` (with `head` at `A`).

1. **Swap the edge:** we need `B` to point back at `A` — do `head.next.next = head`.
2. **Before doing that, save the rest of the list:** changing `B.next` would lose access to everything after `B`. Save `next_node = head.next.next` *before* the assignment in step 1. (Note: `head.next.next` means different things depending on whether it's used before or after the `=` — before, it's the target being *assigned to*; after, it's a value being *read*.)
3. **Preserve a way to reconnect A later:** after `B` points back to `A`, `A` still points to `B` (unchanged so far) — not what we want long-term, but we need to move on to the next pair first. Save `prev = head` (still pointing at `A` at this point) before advancing. Then move to the next pair with `head = next_node`.
4. **Reconnect the previous pair to the rest of the list:** once at the next pair `C -> D`, connect `prev.next = head.next` — this sets `A.next = D` (since `head` is now `C`, `head.next` is `D`).
5. **Track what to return:** by the end, we need to return `B` (the new head of the whole reversed-pairs list) — but the reference to `B` was lost early on. Save it in a `dummy` variable *before* the algorithm starts.
6. **Handle odd-length lists:** step 4 sets `A.next` to `C.next`, but what if there's no `C` (only 3 nodes total)? Before moving to the next pair, also set `head.next = next_node` (i.e. `A.next = C`) as a fallback. If a next pair *does* exist, step 4 will simply override this on the next iteration; if not, this fallback is what sticks.

Since step 2 requires `head.next.next`, the while loop must check **both** `head` and `head.next` — meaning if only one node remains, the loop ends after the current iteration, leaving the step-6 fallback intact (not overridden).

## Code
```python
class Solution:
    def swapPairs(self, head: ListNode) -> ListNode:
        # Check edge case: linked list has 0 or 1 nodes, just return
        if not head or not head.next:
            return head

        dummy = head.next               # Step 5
        prev = None                     # Initialize for step 3
        while head and head.next:
            if prev:
                prev.next = head.next   # Step 4
            prev = head                 # Step 3

            next_node = head.next.next  # Step 2
            head.next.next = head       # Step 1

            head.next = next_node       # Step 6
            head = next_node            # Move to next pair (Step 3)

        return dummy
```

**Note:** the order the steps were *reasoned out* in (above) isn't the same as the order they *execute* in the code — a common theme in linked list problems (see [[Linked Lists - Reversing a Linked List]]).

## Complexity
**O(n) time** (n = number of nodes, while loop runs n times with O(1) work per iteration), **O(1) space** (only a few pointers used).

## General advice
Break the problem down: list everything you need to accomplish and how to achieve each piece. On LeetCode, a wrong-answer submission will point out missed steps; in an interview, talk through your reasoning out loud so the interviewer can help fill gaps. Working through a concrete example (e.g. `1 -> 2 -> 3 -> 4`) with pen and paper is extremely helpful.

#dsa #algorithms #linked-lists

Related: [[Linked Lists - Reversing a Linked List]], [[Linked Lists - Pointer Mechanics]]
