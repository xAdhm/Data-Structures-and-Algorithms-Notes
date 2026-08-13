# Heaps - Top K Pattern

A common interview problem shape: find the **k best** elements, where "best" is defined however the problem specifies.

## Naive approach
Sort the whole input by the problem's criteria, then take the top `k`. **O(n log n) time**, where `n` = input length.

## Heap-based improvement: O(n log k)
Since `k < n` (logically, though `log` is fast enough in practice that this rarely matters much for real speed), a heap-based approach shaves the complexity down — and this small optimization is exactly the kind of thing interviewers look for.

## The technique
1. Create a **min heap**.
2. Iterate over the input, pushing every element onto the heap (scored by the problem's criteria).
3. Whenever the heap's size exceeds `k`, pop from it.

Because the heap is a **min heap** and pops remove the smallest-scored element, popping removes the **"worst"** element by the problem's criteria each time. Since the heap's size is capped at `k`, every heap operation costs at most **O(log k)** — multiplied across `n` iterations gives **O(n log k)** total.

**Why the k best elements survive:** if some element `x` truly belongs in the final top-k answer, it can never get popped — popping only happens when the heap exceeds size `k`, and only removes the *current* minimum. If `x` were popped, that would mean at least `k` other elements in the heap all score higher than `x` — directly contradicting the premise that `x` is one of the k best.

## Worked examples
- [[Heaps - Top K Frequent Elements Example]] — score by frequency
- [[Heaps - Find K Closest Elements Example]] — score by distance, with a max heap and tie-breaking

#dsa #algorithms #heaps

Related: [[Heaps - Overview]], [[Hashing - Hash Maps]]
