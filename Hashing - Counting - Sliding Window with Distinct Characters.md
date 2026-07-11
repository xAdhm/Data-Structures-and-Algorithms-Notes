# Hashing - Counting - Sliding Window with Distinct Characters

Shows how a hash map extends [[Sliding Window - Overview|sliding window]] to handle constraints involving **multiple** distinct elements — see [[Hashing - Counting Overview]] for why this matters.

## Example: Longest substring with at most k distinct characters
Given string `s` and integer `k`, find the length of the longest substring with at most `k` distinct characters.

Example: `s = "eceba"`, `k = 2` → answer is 3 (`"ece"`).

**Why sliding window:** the problem involves substrings with a constraint (at most k distinct characters) — classic sliding window signal (see [[Subarrays and Substrings - Recognizing Patterns]]).

**Why a hash map:** checking "how many distinct characters are in the window" naively costs O(n) per check (scanning the whole window). A hash map makes this check **O(1)**.

## Approach
Maintain a hash map `counts` mapping each character in the window to its frequency.
- **Number of distinct characters in the window = number of keys in `counts`** (checkable in O(1) via the map's length)
- Adding a character (expanding right): increment its count
- Removing a character (shrinking left): decrement its count; if it hits 0, **delete the key** (so the key count accurately reflects distinct characters present)

## Code
```python
from collections import defaultdict

def find_longest_substring(s, k):
    counts = defaultdict(int)
    left = ans = 0
    for right in range(len(s)):
        counts[s[right]] += 1
        while len(counts) > k:
            counts[s[left]] -= 1
            if counts[s[left]] == 0:
                del counts[s[left]]
            left += 1

        ans = max(ans, right - left + 1)

    return ans
```

Note: Python's `collections.defaultdict` behaves like a regular hash map but auto-initializes missing keys (here, to `0` via `int`), avoiding manual existence checks before incrementing.

## Complexity
- **Time: O(n)** — same reasoning as any sliding window: work per for-loop iteration is amortized O(1), since hash map operations are O(1) (see [[Sliding Window - Why It's Efficient]])
- **Space: O(k)** — the hash map never holds more than `k` distinct characters at once, since entries are deleted as soon as the window shrinks past the constraint

#dsa #algorithms #hashing #hash-map #counting #sliding-window

Related: [[Hashing - Counting Overview]], [[Sliding Window - Dynamic Window Size]]
