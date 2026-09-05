# Modular Arithmetic - Divisibility Array Example

## Problem: 2575. Find the Divisibility Array of a String
Given digit string `word` (length `n`) and integer `m`: return `div` where `div[i] = 1` if the numeric value of `word[0..i]` is divisible by `m`, else `0`.

## Why the naive approach fails
Simplest idea: at each index `i`, convert the prefix `word[0..i]` to an actual integer and check divisibility. But converting a string of length `i` to an integer costs **O(i)** — summed across all prefixes (`1 + 2 + ... + n`), this is **O(n²)** total, too slow for `n ≤ 10^5`.

## First improvement: build the prefix incrementally
Instead of reconverting from scratch each time, maintain a running integer `curr` and "append" one digit at a time: `curr = curr * 10 + digit`. This means only ever converting single-character strings — but `curr` itself still grows without bound.

## The real problem: the number gets impossibly large
Since every digit increases the number's magnitude, by the end `curr` could be on the order of `10^(10^5)` — a number with 100,000 digits. Far beyond what any fixed-size integer type could hold (even a 64-bit `long long` maxes out around `10^19`), and far too slow to compute with even in a language without overflow.

## The fix: modular arithmetic
Since the problem only cares whether each prefix is **divisible by `m`** — not the prefix's actual value — apply `% m` at every step: `curr = (curr * 10 + digit) % m`. Per [[Modular Arithmetic - Overview]], this doesn't change divisibility results at any point, while keeping `curr` bounded to values less than `m` throughout — never large, regardless of how long `word` is.

## Code
```python
class Solution:
    def divisibilityArray(self, word: str, m: int) -> List[int]:
        div = []
        curr = 0

        for digit in word:
            curr = (curr * 10 + int(digit)) % m
            if curr == 0:
                div.append(1)
            else:
                div.append(0)

        return div
```

## Complexity
**O(n) time, O(1) extra space** (beyond the output array itself) — `n = len(word)`. A dramatic improvement over the O(n²) naive approach, made possible entirely by recognizing that modular arithmetic preserves divisibility checks at every intermediate step.

#dsa #algorithms #modular-arithmetic #string-building

Related: [[Modular Arithmetic - Overview]], [[String Building - O(n) Technique]]
