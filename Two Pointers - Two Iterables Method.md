# Two Pointers - Two Iterables Method

**Idea:** applicable when a problem has two iterables as input (e.g. two arrays). Move a pointer along each input simultaneously until all elements have been checked.

## Steps
1. Create two pointers, `i` and `j`, each starting at index 0 — one per iterable
2. Loop `while i < arr1.length AND j < arr2.length`
3. Each iteration: do problem-specific logic, then move pointers forward — increment `i`, `j`, or both
4. When the loop ends, one pointer may not have reached the end of its iterable yet. If the problem requires processing *every* element of both inputs, add follow-up loops to exhaust whichever pointer is left over (only one of these runs, since the main loop only stops when at least one pointer is exhausted)

## Pseudocode
```
function fn(arr1, arr2):
    i = j = 0
    while i < arr1.length AND j < arr2.length:
        Do some logic here depending on the problem
        Do some more logic here to decide on one of the following:
            1. i++
            2. j++
            3. Both i++ and j++

    // Step 4: make sure both iterables are exhausted
    // Note that only one of these loops would run
    while i < arr1.length:
        Do some logic here depending on the problem
        i++

    while j < arr2.length:
        Do some logic here depending on the problem
        j++
```

## Why it's O(n + m)
If work per iteration is O(1), this runs in **O(n + m)** time, where `n = arr1.length`, `m = arr2.length` — at least one pointer advances every iteration, and neither can advance more than its own array's length before the arrays are exhausted.

---

## Example 3: Merge two sorted arrays
**Problem:** given two sorted integer arrays `arr1` and `arr2`, return a new sorted array combining both.

**Brute force:** concatenate then sort → if `n = arr1.length + arr2.length`, this costs **O(n·log n)**. Reasonable if the inputs weren't sorted, but wasteful here.

**Two pointers approach:** since both inputs are already sorted, build the answer one element at a time. Start a pointer at index 0 of each array. At each step, compare the two pointed-at values, append the smaller one to the answer array, and advance that pointer. Repeat, then dump any remaining elements from whichever array still has some.

**Complexity:** O(n) time, O(1) extra space (not counting the output array, which is the usual convention).

**Aside — variable naming:** here `n` is redefined as `arr1.length + arr2.length` (the *combined* length), rather than `n` and `m` as separate lengths (as in [[Two Pointers - Converging Pointers Method]]'s Example 2). Big O lets you define variables however makes sense — since the arrays are being combined, treating the total as one meaningful quantity (`n`) is a reasonable choice. Either convention is valid; it doesn't change the actual complexity, just how it's expressed.

---

## Example 4: Is Subsequence
**Problem:** given strings `s` and `t`, return true if `s` is a subsequence of `t`.
(LeetCode 392. Is Subsequence)

A subsequence = characters obtainable by deleting some (or no) characters from the original while preserving relative order. E.g. `"ace"` is a subsequence of `"abcde"`; `"aec"` is not (wrong order).

**Two pointers approach:**
- `i` tracks position in `s`, `j` tracks position in `t`
- If `s[i] == t[j]`, that character of `s` has been "found" — increment `i`
- Increment `j` every iteration regardless (this also means the algorithm could be implemented with a plain for loop over `t`)
- `s` is a subsequence of `t` if, by the end, `i == s.length` (every character of `s` was found in order)

**Complexity:** O(1) space; time is linear in the lengths of `s` and `t`.

#dsa #algorithms #two-pointers #arrays #strings

Related: [[Two Pointers - Overview]], [[Two Pointers - Converging Pointers Method]]
