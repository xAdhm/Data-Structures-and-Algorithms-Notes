# Stacks - Remove Adjacent Duplicates Example

## Problem: 1047. Remove All Adjacent Duplicates In String
Given string `s`, continuously remove adjacent duplicate character pairs until none remain, and return the final string.

Example: `"abbaca"` → remove `"bb"` → `"aaca"` → remove `"aa"` → `"ca"` (final answer).

## Recognizing the LIFO pattern
The tricky part: not all removable pairs are visible from the start. In `"abbaca"`, the `"aa"` pair only becomes adjacent *after* `"bb"` is removed. Consider `"abccba"` — the deletion order needed is `c → b → a`: the **most recently encountered** character is the first one that needs to be resolved (deleted), which is the LIFO signal for [[Stacks - Overview|a stack]].

The characters between a matching pair (e.g. `b` and `c` sitting between the two `a`s in `"abccba"`) are "in the way" — they must be resolved first, in reverse order of how they were encountered.

## Approach
Iterate over the string, maintaining a stack:
- If the top of the stack matches the current character → they're adjacent (at this point in the process) → **pop** the stack (delete both).
- Otherwise → **push** the current character.

The stack naturally maintains the correct "in the way" ordering — the most recently pushed character is always the first eligible for a match/deletion.

## Code
```python
class Solution:
    def removeDuplicates(self, s: str) -> str:
        stack = []
        for c in s:
            if stack and stack[-1] == c:
                stack.pop()
            else:
                stack.append(c)

        return "".join(stack)
```

**Language note:** since stacks are defined purely by their interface (add/remove from the same end — see [[Stacks - Overview]]), some languages can use a more specialized structure directly — e.g. C++ strings are mutable, so a string itself can serve as the stack; Java can use `StringBuilder` for the same convenience, since it converts easily back to a string at the end.

## Complexity
**O(n) time and O(n) space**, where `n` = length of the input — stack operations here are all O(1), and the stack can grow up to size `n` in the worst case (no deletions at all).

#dsa #algorithms #stacks #strings

Related: [[Stacks - Overview]], [[Stacks - Valid Parentheses Example]]
