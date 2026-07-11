# Hashing - Counting - Frequency Map Examples

Two examples of building a full frequency map (no sliding window needed) and reasoning directly about the counts. See [[Hashing - Counting Overview]].

---

## Example: Intersection of Multiple Arrays
**Problem:** given a 2D array `nums` containing `n` arrays of **distinct** integers, return a sorted array of all numbers appearing in every one of the `n` arrays. (LeetCode 2248)

Example: `nums = [[3,1,2,4,5],[1,2,3,4],[3,4,5,6]]` → `[3, 4]`

**Key insight:** since each individual array has distinct integers, a number appears exactly `n` times overall **if and only if** it appears in all `n` arrays.

**Approach:** count frequency of every element across all arrays with a hash map, then collect keys whose count equals `n`.

```python
from collections import defaultdict

class Solution:
    def intersection(self, nums: List[List[int]]) -> List[int]:
        counts = defaultdict(int)
        for arr in nums:
            for x in arr:
                counts[x] += 1

        n = len(nums)
        ans = []
        for key in counts:
            if counts[key] == n:
                ans.append(key)

        return sorted(ans)
```

**Why not just use an array instead of a hash map?** Since keys are integers, you could try an array indexed by value — but the array would need to be sized to the *maximum* possible element. E.g. input `[1, 2, 3, 1000]` would need an array of size 1001, almost entirely unused — wasteful. A hash map handles arbitrarily large values (even `99999999999`) without needing to know the range up front. Arrays can sometimes be more efficient due to hash map overhead, but hash maps are the safer general default.

**Complexity:**
Let `n` = number of lists, `m` = average elements per list.
- Populating the hash map: O(n·m)
- Iterating over unique keys to build `ans`: up to O(n·m) in the worst case (all elements unique) — doesn't change overall complexity since the first loop already costs that much
- Sorting `ans` (at most `m` elements in the worst case where all are unique): O(m·log m)
- **Total time: O(n·m + m·log m) = O(m·(n + log m))**
- **Space: O(n·m)** in the worst case (all elements unique, so the hash map grows to that size)

---

## Example: Check if All Characters Have Equal Number of Occurrences
**Problem:** given string `s`, determine if all characters appear the same number of times. (LeetCode 1941)

Example: `s = "abacbc"` → true (each character appears twice). `s = "aaabb"` → false (3 vs 2).

**Approach:** build a frequency map of characters, then check whether all the frequency *values* are identical. Since a [[Hashing - Sets|set]] ignores duplicates, dumping all frequency values into a set and checking `len(set) == 1` confirms whether there's only one unique frequency.

```python
from collections import defaultdict

class Solution:
    def areOccurrencesEqual(self, s: str) -> bool:
        counts = defaultdict(int)
        for c in s:
            counts[c] += 1

        frequencies = counts.values()
        return len(set(frequencies)) == 1
```

**Bonus — Python one-liner using `Counter`:**
```python
from collections import Counter

class Solution:
    def areOccurrencesEqual(self, s: str) -> bool:
        return len(set(Counter(s).values())) == 1
```

**Complexity:** with `n` = length of `s` — O(n) to build the hash map, O(n) to convert values to a set → **O(n) total time**.
**Space:** proportional to the number of *unique* characters. Common interview answer: O(1) since input is bounded to the English alphabet (a constant, 26). More general answer: **O(k)**, where `k` is the number of possible characters in the input alphabet (26 in this specific problem).

#dsa #algorithms #hashing #hash-map #counting #sets

Related: [[Hashing - Counting Overview]], [[Hashing - Sets]], [[Hashing - Checking for Existence]]
