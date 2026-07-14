# Hashing - Group Anagrams Example

## Problem: 49. Group Anagrams
Given an array of strings `strs`, group the anagrams together.

Example: `strs = ["eat","tea","tan","ate","nat","bat"]` → `[["bat"],["nat","tan"],["ate","eat","tea"]]`

## The core idea: give every group an "identifier"
Checking if two strings are anagrams pairwise (e.g. comparing two frequency hash maps) is cumbersome and doesn't scale to grouping more than 2 strings at once. Instead: find a value that's **identical for every string in a group**, and use that as a hash map key.

**Two strings are anagrams if and only if they're equal after sorting.** Sorting forces characters into a fixed, well-defined order — anagrams share the same letters, so sorted, they must produce the same string. E.g. `"bcab"` sorted → `"abbc"`; every anagram of `"bcab"` also sorts to `"abbc"`.

So: sort each string to get its group identifier, then map `identifier → list of original strings` in a hash map. The answer is just the hash map's values.

## Code
```python
from collections import defaultdict

class Solution:
    def groupAnagrams(self, strs: List[str]) -> List[List[str]]:
        groups = defaultdict(list)
        for s in strs:
            key = "".join(sorted(s))
            groups[key].append(s)

        return list(groups.values())
```

**Python note:** `dict.values()` returns a *view* object, not a list — wrap it in `list(...)` if a list is required.

## Complexity
Let `n = len(strs)`, `m` = average string length.
- Sorting each string: O(n · m · log m)
- Iterating over the resulting groups: O(n) in the worst case (all unique, n groups) — dominated by the sort cost
- **Total time: O(n · m · log m)**
- **Space: O(n · m)** — every string ends up stored in some group's list

## Alternative: character-count tuple instead of sorted string
Instead of sorting, use a length-26 tuple of character counts as the key. This gets **O(n·m)** time (no `log m` sorting factor) — technically better, but:
- For small strings, the constant factor (building a 26-length tuple every time) can make it *slower in practice* than sorting, since Big O hides constants (see [[Big O - Rules for Calculating Complexity]])
- Less general — assumes only 26 possible characters, which is valid here but wouldn't hold up well for follow-up variations

#dsa #algorithms #hashing #hash-map

Related: [[Hashing - Hash Maps]], [[Hashing - Max Sum Equal Digit Sum Example]]
