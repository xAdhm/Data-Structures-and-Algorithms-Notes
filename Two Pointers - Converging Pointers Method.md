# Two Pointers - Converging Pointers Method

**Idea:** start pointers at the edges of the input and move them toward each other until they meet.

## Steps
1. `left = 0`, `right = arr.length - 1`
2. Loop `while left < right`
3. Each iteration: do problem-specific logic, then move pointers closer — increment `left`, decrement `right`, or both (depends on the problem)

## Pseudocode
```
function fn(arr):
    left = 0
    right = arr.length - 1

    while left < right:
        Do some logic here depending on the problem
        Do some more logic here to decide on one of the following:
            1. left++
            2. right--
            3. Both left++ and right--
```

## Why it's O(n)
The pointers start `n` apart and move at least one step closer every iteration, so the loop can never run more than O(n) times. If each iteration is O(1), total time complexity is O(n).

---

## Example 1: Valid Palindrome
**Problem:** given a string `s`, return true if it's a palindrome (reads the same forward and backward).

**Approach:** if a string is a palindrome, its first character equals its last, its second equals its second-to-last, and so on. Use two pointers starting at the first and last characters, compare, then move both inward one step at a time. Continue until pointers meet or a mismatch is found.

Works identically on an array of characters — two pointers just needs an abstract iterable to move along, not specifically a string.

**Complexity:** O(n) time, O(1) space — regardless of input size, only two integer variables are used.

---

## Example 2: Two Sum II (sorted input, existence check)
**Problem:** given a **sorted** array of unique integers and a target, return true if any pair sums to target.
Example: `nums = [1, 2, 4, 6, 8, 9, 14, 15]`, `target = 13` → true (4 + 9 = 13).
(LeetCode 167. Two Sum II - Input Array Is Sorted)

**Brute force:** check all pairs → O(n²).

**Two pointers approach (O(n), since array is sorted):**
Start `left` at index 0, `right` at the last index.
- If `nums[left] + nums[right] > target` → sum too big → move `right` left (decreases the sum)
- If `nums[left] + nums[right] < target` → sum too small → move `left` right (increases the sum)
- If equal → found it

**Why it works:** because the array is sorted, moving `left` forward can only *increase* `nums[left]`, and moving `right` backward can only *decrease* `nums[right]`. If `x + y > target`, no solution can involve keeping `y` as-is (since `x` can only grow) — so `y` must shrink, meaning move `right`. Symmetric logic applies if the sum is too small.

**Complexity:** O(n) time, O(1) space.

#dsa #algorithms #two-pointers #arrays #strings

Related: [[Two Pointers - Overview]], [[Two Pointers - Two Iterables Method]]
