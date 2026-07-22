# Monotonic Stacks - Daily Temperatures Example

## Problem: 739. Daily Temperatures
Given daily `temperatures`, return `answer` where `answer[i]` = number of days after day `i` until a warmer temperature. If none exists, `answer[i] = 0`.

## Why brute force is wasteful
Brute force: for each day, scan forward until a warmer day is found — O(n²). Key inefficiency, illustrated by `temperatures = [34, 33, 32, 31, 30, 50]`: all of the first 5 days share the same answer day (day 6).

**The transitive insight:** if `33` isn't warmer than `34`, and `32` isn't warmer than `33`, then `32` also isn't warmer than `34` (transitivity: `32 ≯ 33 ≯ 34`). This means there's no point checking whether something is warmer than `34` **until** we've already found something warmer than `33` — we can defer checking earlier elements until later elements get resolved first. That "process later, defer earlier" behavior is the LIFO signal for [[Monotonic Stacks and Queues - Overview|a monotonic stack]].

## Approach
Maintain a monotonically **decreasing** stack (of indices, since we need the *distance* between days, and the actual temperature is recoverable via `temperatures[index]`):
- For each day `curr`, compare it against the temperature at the top of the stack.
- While `curr` is warmer than the top: pop it — `curr` is the answer for that popped day (first day warmer than it). Compute `answer[popped_index] = curr_index - popped_index`.
- Push `curr`'s index onto the stack.

Because the stack is kept monotonically decreasing, the top of the stack is always the **coldest** unresolved day — exactly the next one that should be checked against an incoming warmer temperature.

## Code
```python
class Solution:
    def dailyTemperatures(self, temperatures: List[int]) -> List[int]:
        stack = []
        answer = [0] * len(temperatures)

        for i in range(len(temperatures)):
            while stack and temperatures[stack[-1]] < temperatures[i]:
                j = stack.pop()
                answer[j] = i - j
            stack.append(i)

        return answer
```

`j` is the index of a day we already passed; `i` is the first day warmer than it; `i - j` is the number of days between them.

## Complexity
**O(n) time** (amortized — each index is pushed once and popped at most once, per [[Monotonic Stacks and Queues - Overview]]), **O(n) space** in the worst case (e.g. strictly decreasing temperatures — nothing ever pops, stack grows to full size).

#dsa #algorithms #stacks #monotonic

Related: [[Monotonic Stacks and Queues - Overview]], [[Stacks - Overview]]
