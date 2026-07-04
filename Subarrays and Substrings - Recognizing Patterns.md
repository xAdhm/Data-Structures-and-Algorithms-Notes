# Subarrays and Substrings - Recognizing Patterns

A subarray/substring is a **contiguous** section of an array/string (see [[Sliding Window - Overview]]).

## When to think "sliding window"
Signals that suggest sliding window (guideline, not a guarantee — not every problem with these traits needs it, and not every sliding window problem has all these traits):

**Explicit constraints in the problem:**
- Sum greater/less than some value `k`
- Limits on contents — e.g. max `k` unique elements, no duplicates allowed

**What the problem asks for:**
- Minimum or maximum length
- Number of subarrays/substrings
- Max or minimum sum

See [[Sliding Window - Dynamic Window Size]], [[Sliding Window - Counting Valid Subarrays]], [[Sliding Window - Fixed Window Size]].

## When to think "prefix sum"
If the input is an integer array and the problem requires calculating **multiple subarray sums**, consider [[Prefix Sum - Overview]] instead (or in addition).

## Useful formula
The size of a subarray from index `i` to `j` (inclusive) is `j - i + 1`.
This is also the number of subarrays that **end at `j`** and start anywhere from `i` onward — the same counting trick used in [[Sliding Window - Counting Valid Subarrays]].

#dsa #algorithms #arrays #strings #sliding-window #prefix-sum

Related: [[Sliding Window - Overview]], [[Prefix Sum - Overview]], [[Subsequences - Overview]], [[Subsets - Overview]]
