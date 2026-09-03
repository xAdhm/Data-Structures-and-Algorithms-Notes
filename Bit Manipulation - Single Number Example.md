# Bit Manipulation - Single Number Example

## Problem: 136. Single Number
Given a non-empty array where every element appears **twice** except one, find the element that appears once.

## Building up to the XOR solution
- **Hash map approach:** count frequencies, find the one with count 1 → **O(n) time, O(n) space**.
- **Sort approach:** sort, then scan for the unpaired element → time becomes **O(n log n)**, though space may improve depending on the sort implementation.
- **XOR approach (optimal):** recall [[Bit Manipulation - Overview|XOR's definition]] — result bit is `1` if the count of `1`s is **odd**. The target number is exactly the one appearing an **odd** number of times (once) in the whole array.

## The key XOR properties
- `x XOR x = 0` — any number XORed with itself cancels to zero.
- `0 XOR y = y` — XORing with zero leaves a number unchanged.

Combining: `x XOR x XOR y = y`.

## Why this works on the whole array
XOR every element in `nums` together. Every number appearing **twice** contributes an `x XOR x` pair, which cancels to `0`. All those zeros XORed together are still `0`. What's left is `0 XOR (the single unpaired number) = that number`.

**Order doesn't matter** — XOR is commutative and associative, so however the array is traversed, the pairs still cancel out identically.

## Code
```python
class Solution:
    def singleNumber(self, nums: List[int]) -> int:
        mask = 0
        for num in nums:
            mask ^= num

        return mask
```

## Complexity
**O(n) time, O(1) space** — a genuine improvement over both the hash map (same time, more space) and sorting (worse time) approaches. **Practically even faster than the hash map version**, since integer/bit operations have far less overhead than hashing.

#dsa #algorithms #bit-manipulation

Related: [[Bit Manipulation - Overview]], [[Hashing - Counting Overview]]
