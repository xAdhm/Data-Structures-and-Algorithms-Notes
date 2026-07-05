# Hashing - Checking for Existence

One of the most common uses of a hash map or [[Hashing - Sets|set]] is checking whether an element exists, in **O(1)**. An array needs O(n) for the same check — swapping in a hash map/set often drops an algorithm's time complexity from **O(n²) to O(n)**.

**Rule of thumb:** anytime your algorithm involves something like `if x in ...` on an array, consider a hash map or set instead, to make that check O(1).

---

## Example 1: Two Sum
**Problem:** given `nums` and `target`, return indices of two numbers that add up to `target`. Can't reuse the same index twice. (LeetCode 1. Two Sum)

**Brute force:** for each number `num`, inner loop to search for `target - num` elsewhere in the array → inner search is O(n) → total **O(n²)**.

**Hash map approach:** build a hash map while iterating, mapping `value → index`. At each index `i` (`num = nums[i]`), check the map for `target - num`. Both the lookup and the insert are O(1).

**Why a hash map, not just a set:** if the problem only asked for a boolean ("does a pair exist?") or the actual numbers, a set would suffice. Because it asks for **indices**, we need to remember *where* each number was seen — hence a hash map (value → index), not just a set.

**Complexity:** O(n) time (hash map ops are O(1)), O(n) space (number of stored keys scales with input size).

```python
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        dic = {}
        for i in range(len(nums)):
            num = nums[i]
            complement = target - num
            if complement in dic: # This operation is O(1)!
                return [i, dic[complement]]

            dic[num] = i

        return [-1, -1]
```

---

## Example 2: First Letter to Appear Twice
**Problem:** given string `s`, return the first character to appear twice. Guaranteed at least one duplicate exists. (LeetCode 2351)

**Brute force:** for each character `c`, inner loop back through everything before it checking for a match → **O(n²)**.

```python
class Solution:
    def repeatedCharacter(self, s: str) -> str:
        for i in range(len(s)):
            c = s[i]
            for j in range(i):
                if s[j] == c:
                    return c
        return ""
```

**Set approach:** maintain a set of characters seen so far. For each character, check the set (O(1)) — if present, that's the answer; if not, add it to the set and continue.

```python
class Solution:
    def repeatedCharacter(self, s: str) -> str:
        seen = set()
        for c in s:
            if c in seen:
                return c
            seen.add(c)
        return " "
```

**Complexity:** O(n) time (each iteration now constant time).

**On space complexity — a subtlety worth knowing for interviews:**
- Common argument: since the input is limited to English alphabet characters (bounded by a constant, 26), space complexity is **O(1)**. This is common for string problems and technically correct.
- More general/technically correct alternative: **O(m)**, where `m` is the number of allowable characters in the input alphabet.
- Either answer is defensible in an interview — just be ready to explain the reasoning behind whichever you give.

---

## Example 3: Numbers with no adjacent value present
**Problem:** given integer array `nums`, find all numbers `x` such that neither `x + 1` nor `x - 1` is in `nums`. If a valid `x` appears multiple times, include it only once in the answer.

**Approach:** convert `nums` into a set beforehand (this is a form of **pre-processing** — see also [[Prefix Sum - Overview]] for another example of the same idea). Then iterate through `nums`, and for each `x`, check whether `x + 1` or `x - 1` is in the set — O(1) per check thanks to the set.

```python
def find_numbers(nums):
    ans = []
    nums_set = set(nums)
    for num in nums_set:
        if (num + 1 not in nums_set) and (num - 1 not in nums_set):
            ans.append(num)

    return ans
```

**Complexity:** O(n) time (each iteration constant time thanks to O(1) set checks), O(n) space (the set).

#dsa #algorithms #hashing #hash-map #sets

Related: [[Hashing - Hash Maps]], [[Hashing - Sets]], [[Prefix Sum - Overview]]
