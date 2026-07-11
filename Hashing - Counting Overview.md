# Hashing - Counting Overview

**Counting** is a very common hash map pattern — tracking the frequency of things. The hash map maps keys to integers (their counts). Anytime a problem involves counting anything, think hash map.

## Why it extends sliding window
In earlier [[Sliding Window - Overview|sliding window]] problems, constraints were often based on a single element (e.g. "at most k zeroes" — tracked with a single integer `curr`). A hash map opens the door to constraints involving **multiple distinct elements** at once — e.g. "at most k *distinct* characters" — since you now need to track the count of each element independently, not just one running total.

## Two counting-related patterns covered
1. **Sliding window + frequency map** — use a hash map inside a sliding window to track counts of multiple elements as the constraint metric. See [[Hashing - Counting - Sliding Window with Distinct Characters]].
2. **Straightforward frequency comparison** — build a full frequency map (no sliding window), then reason about the counts directly. See [[Hashing - Counting - Frequency Map Examples]].

There's also a related, more advanced pattern combining counting with prefix sums for **exact-value subarray constraints** — see [[Hashing - Subarray Sum Equals K (Exact Constraint Pattern)]].

#dsa #algorithms #hashing #hash-map #counting

Related: [[Hashing - Hash Maps]], [[Sliding Window - Overview]]
