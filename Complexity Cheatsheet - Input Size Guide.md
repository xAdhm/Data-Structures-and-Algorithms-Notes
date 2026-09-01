# Complexity Cheatsheet - Input Size Guide

Problem constraints hint at the expected time complexity — an upper bound your solution should stay under. On LeetCode/OAs, constraints are usually given explicitly; in interviews, they're often unstated but worth asking about.

## n ≤ 10
Expected complexity likely involves a **factorial** or an **exponential with base > 2** — e.g. O(n²·n!) or O(4ⁿ). Think [[Backtracking - Overview|backtracking]] or brute-force-esque recursion. This bound is tiny — most correct algorithms will be fast enough regardless.

## 10 < n ≤ 20
Expected complexity likely **O(2ⁿ)**. Anything with a higher base or a factorial will be too slow (3²⁰ ≈ 3.5 billion; 20! is astronomically larger). O(2ⁿ) typically signals "considering all subsets/subsequences" — each element has a binary take-or-don't-take choice (see [[Backtracking - Subsets Example]]). Still small enough that most correct approaches pass — consider backtracking/recursion.

## 20 < n ≤ 100
Exponentials become too slow here. Expected upper bound is likely **O(n³)**.

**Deceptive trap:** LeetCode "easy" problems often sit in this range — a linear O(n) solution might exist, but the small bound also lets brute-force nested loops pass (finding the truly optimal solution might not have felt "easy"). Consider nested-loop brute force first, then analyze which steps are "slow" and look for hash map/heap-based improvements.

## 100 < n ≤ 1,000
**O(n²)** should be sufficient, assuming a reasonably small constant factor. Similar to the previous range (nested loops), but here O(n²) is often the actual expected/optimal complexity — may not be improvable further.

## 1,000 < n < 100,000
`n ≤ 10⁵` is the **most common LeetCode constraint**. Slowest generally-acceptable complexity: **O(n log n)**, though **O(n)** is often the real goal.

Ask: would sorting or a heap help? If not, aim for O(n). **O(n²) nested loops are unacceptable here** — likely need one of these techniques to collapse an O(n²) shape into O(n) or O(n log n):
- [[Hashing - Hash Maps|Hash map]]
- [[Two Pointers - Overview|Two pointers]] / [[Sliding Window - Overview|sliding window]]
- [[Monotonic Stacks and Queues - Overview|Monotonic stack]]
- [[Binary Search - Overview|Binary search]]
- [[Heaps - Overview|Heap]]
- Some combination of the above

If you land on O(n), the constant factor can reasonably be as large as ~40. Common string-problem pattern: looping over the alphabet (26 letters) at each iteration → effectively **O(26n)**.

## 100,000 < n < 1,000,000
`n ≤ 10⁶` is a **rarer** constraint, usually demanding **O(n)**. O(n log n) is generally still safe if its constant factor is small. A [[Hashing - Hash Maps|hash map]] is very likely needed somewhere in the solution.

## n > 1,000,000
For huge inputs (often 10⁹+), the acceptable complexity is typically **O(log n)** or **O(1)**. Requires either drastically shrinking the search space each step (usually [[Binary Search - Overview|binary search]]) or clever constant-time tricks (math, or a clever hash map use). O(√n) is possible but rare, mostly in advanced problems.

#dsa #algorithms #big-o #reference

Related: [[Complexity Cheatsheet - By Data Structure]], [[Big O - Rules for Calculating Complexity]]
