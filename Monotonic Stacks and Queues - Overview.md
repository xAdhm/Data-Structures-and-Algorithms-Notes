# Monotonic Stacks and Queues - Overview

⚠️ One of the more difficult concepts in this course — not super common in interviews, but worth knowing. Okay to move on and revisit later if stuck.

**Monotonic** (of a function/quantity): varying so that it never decreases, or never increases.

A **monotonic stack or queue** is one whose elements are always kept sorted (ascending or descending, depending on the problem). The sorted property is maintained by **removing elements that would violate it before adding new ones**.

## Example: maintaining a monotonic increasing stack
`stack = [1, 5, 8, 15, 23]`, want to push `14`. To preserve increasing order, first pop `23` and `15` (both larger than 14), *then* push: `stack = [1, 5, 8, 14]`.

## General template
```
Given an integer array nums

stack = []
for num in nums:
    while stack.length > 0 AND stack.top > num:
        stack.pop()
    // Between the above and below lines, do some logic depending on the problem
    stack.push(num)
```

**Time complexity — still O(n)**, despite the nested loop: same amortized reasoning as [[Sliding Window - Why It's Efficient]] — the inner while loop can only pop each element once, total, across the *entire* run, so the for loop is amortized O(1) per iteration.

## When to reach for this pattern
- Problems asking, for each element, to find the "next" element satisfying some criteria (e.g. "next greater element")
- Problems with a **dynamic window** of elements where you need to track the max/min as the window changes
- Sometimes only *part* of a more advanced algorithm

## Connecting back to the string-problems chapter
The [[Stacks - Overview|stack]] chapter's string problems ([[Stacks - Valid Parentheses Example]], [[Stacks - Remove Adjacent Duplicates Example]], [[Stacks - Backspace String Compare Example]]) all shared a theme: elements needed to be "operated on" eventually, but **not immediately** — they had to wait. Monotonic stacks/queues extend this same idea: an element sits and waits until the right condition (e.g. a warmer temperature, a larger number) comes along to resolve it.

## Worked examples
- [[Monotonic Stacks - Daily Temperatures Example]] — monotonic **decreasing stack**, "next greater element" pattern
- [[Monotonic Queues - Sliding Window Maximum Example]] — monotonic **decreasing deque**, tracking max in a sliding window
- [[Monotonic Queues - Longest Subarray With Limit Example]] — **two deques** (one increasing, one decreasing) combined with standard sliding window

## A terminology nuance
Technically, "monotonically decreasing" implies *strictly* decreasing (no equal adjacent elements) — something like `[5, 3, 3, 2]` wouldn't qualify. The more precise term when equal elements are allowed is "monotonically **non-increasing**." This course uses "decreasing" loosely for simplicity — the important property is that the stack/queue stays sorted, not strict inequality. To enforce strict inequality (no equal elements) in your own implementation, swap `>`/`<` comparisons for `>=`/`<=`.

#dsa #algorithms #stacks #queues #monotonic

Related: [[Stacks - Overview]], [[Queues - Overview]], [[Sliding Window - Why It's Efficient]]
