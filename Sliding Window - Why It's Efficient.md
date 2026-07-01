# Sliding Window - Why It's Efficient

## The brute force baseline
For an array of length `n`, the total number of subarrays is:

n + (n-1) + (n-2) + ... + 1 = n(n+1)/2

(the partial sum of 1 to n). Any algorithm that examines every subarray individually is therefore **at least O(n²)** — usually too slow.

## Why sliding window avoids this
A sliding window guarantees at most **2n** total window-boundary movements across the *entire* algorithm:
- `right` can move forward at most `n` times
- `left` can move forward at most `n` times

So if the work done per window (per iteration) is O(1), the whole algorithm runs in **O(n)** — dramatically better than examining every subarray individually.

## "But there's a while loop inside a for loop — isn't that O(n²)?"
No — this is **amortized analysis**. The inner `while` loop (which moves `left`) can only execute a *total* of `n` times across the *entire* run of the algorithm, because `left` starts at 0, only ever increases, and can never exceed `n`.

If the while loop happened to run `n` times during one particular iteration of the outer for loop, that would mean it *doesn't* run at all during the other iterations — the total work is still bounded by `n` across the whole algorithm, not `n` work per outer iteration.

So even though a single for-loop iteration could theoretically cost O(n) in the worst case, the cost **averages out to O(1) per iteration** once you account for the entire runtime — hence "amortized O(1)."

#dsa #algorithms #sliding-window #big-o #amortized-analysis

Related: [[Sliding Window - Overview]], [[Big O - Rules for Calculating Complexity]], [[Arrays and Strings - Time Complexity of Operations]]
