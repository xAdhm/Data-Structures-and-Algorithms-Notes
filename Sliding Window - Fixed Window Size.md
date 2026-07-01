# Sliding Window - Fixed Window Size

Some problems specify a **fixed** window length `k`, instead of a dynamic one (contrast with [[Sliding Window - Dynamic Window Size]]).

These are simpler: the difference between any two adjacent windows is always exactly two elements — one added on the right, one removed on the left, to keep the length constant at `k`.

## Approach
1. Build the first window from index `0` to `k - 1`
2. Slide forward one index at a time: when adding element at index `i`, remove the element at index `i - k`

Example: `k = 2`, current window covers indices `[0, 1]`. Add index `2` → `[0, 1, 2]` → remove index `2 - k = 0` → window is now `[1, 2]`.

## General template
```
function fn(arr, k):
    curr = some data to track the window

    // build the first window
    for (int i = 0; i < k; i++)
        Do something with curr or other variables to build first window

    ans = answer variable, probably equal to curr here depending on the problem
    for (int i = k; i < arr.length; i++)
        Add arr[i] to window
        Remove arr[i - k] from window
        Update ans

    return ans
```

---

## Example 4: Max sum subarray of fixed length k
Given an integer array `nums` and integer `k`, find the sum of the subarray with the largest sum among all subarrays of length exactly `k`.

Approach: build the first window of length `k`, initialize the answer to that window's sum (`curr`), then slide: for each new index `i`, add `nums[i]` and remove `nums[i - k]`, updating the answer as needed.

**Complexity:** O(n) time (n = length of nums, constant work per iteration), O(1) space.

#dsa #algorithms #sliding-window #arrays

Related: [[Sliding Window - Overview]], [[Sliding Window - Dynamic Window Size]]
