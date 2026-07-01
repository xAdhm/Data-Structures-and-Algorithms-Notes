# Sliding Window - Dynamic Window Size

Covers the standard implementation for problems asking for the **best** valid subarray (e.g. longest), where the window size grows and shrinks dynamically. See [[Sliding Window - Overview]] for the core concept.

## Implementation logic
- **Don't** literally store the window's elements in a separate array — that makes adding/removing/summing O(n) per operation.
- Instead, track the constraint metric with a single variable, e.g. `curr`:
  - Adding element from the right: `curr += nums[right]`
  - Removing element from the left: `curr -= nums[left]`
  - Both operations are O(1)
- The window itself is conceptual — only `left`, `right`, and `curr` are actually maintained.
- `right` only ever moves forward → drive it with a **for loop**.
- `left` only moves forward when the window is invalid → drive it with a **while loop** nested inside the for loop, with condition `while WINDOW_IS_INVALID`.
- After the while loop (window guaranteed valid), update the answer. **Window length formula: `right - left + 1`** — memorize this.

## General template
```
function fn(arr):
    left = 0
    for (int right = 0; right < arr.length; right++):
        Do some logic to "add" element at arr[right] to window

        while WINDOW_IS_INVALID:
            Do some logic to "remove" element at arr[left] from window
            left++

        Do some logic to update the answer
```

---

## Example 1: Longest subarray with sum ≤ k
`nums = [3, 1, 2, 7, 4, 2, 1, 1, 5]`, `k = 8`

```
function fn(nums, k):
    left = 0
    curr = 0
    answer = 0
    for (int right = 0; right < nums.length; right++):
        curr += nums[right]
        while (curr > k):
            curr -= nums[left]
            left++

        answer = max(answer, right - left + 1)

    return answer
```

Walkthrough: window grows to `[3,1,2]` (valid), adding `7` breaks it → shrink down to `[7]` alone, still can't grow past that without breaking → shrink to `[4]`, grows to `[4,2,1,1]` (valid, length 4), next addition breaks it → shrink to `[1,1,5]`. Longest valid window found: `[4,2,1,1]` → **answer = 4**.

**Complexity:** O(n) time (all for-loop work is amortized O(1) — see [[Sliding Window - Why It's Efficient]]), O(1) space (only a few integer variables, no matter the input size).

---

## Example 2: Longest substring with at most one "0"
Binary string `s`, may flip up to one `"0"` to `"1"`. Find the longest achievable run of all `"1"`s.

Example: `s = "1101100111"` → answer is 5 (flip index 2 → `"1111100111"`).

Reframe: this is equivalent to "find the longest substring containing at most one `0`" — a direct sliding window constraint: `window.count("0") <= 1`. Track it with an integer `curr` counting zeroes currently in the window; shrink whenever `curr > 1`.

**Complexity:** O(n) time (n = length of s), O(1) space.

#dsa #algorithms #sliding-window #arrays #strings

Related: [[Sliding Window - Overview]], [[Sliding Window - Counting Valid Subarrays]], [[Sliding Window - Why It's Efficient]]
