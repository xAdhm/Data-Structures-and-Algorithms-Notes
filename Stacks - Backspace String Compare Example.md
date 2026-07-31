# Stacks - Backspace String Compare Example

## Problem: 844. Backspace String Compare
Given strings `s` and `t`, where `'#'` represents a backspace, determine if they're equal once typed into a text editor (backspaces applied).

Example: `s = "ab#c"`, `t = "ad#c"` → both simplify to `"ac"` → true.

## Recognizing the LIFO pattern
A backspace deletes the **most recently typed** character — exactly LIFO, and exactly what [[Stacks - Overview|a stack]] naturally models: push characters as they're typed, and a backspace just pops the top.

## Approach
Simulate typing each string using a stack:
- Regular character → push onto the stack
- `'#'` → pop the stack (careful: only if the stack isn't already empty — backspacing on nothing should just do nothing)

Build the final simplified string for both `s` and `t` this way, then compare.

## Code
```python
class Solution:
    def backspaceCompare(self, s: str, t: str) -> bool:
        def build(s):
            stack = []
            for c in s:
                if c != "#":
                    stack.append(c)
                elif stack:
                    stack.pop()
            return "".join(stack)
        return build(s) == build(t)
```

## Complexity
**O(n) time and O(n) space**, linear in the input sizes — same reasoning as the other stack-based string problems: O(1) stack operations, stack size bounded by input length.

#dsa #algorithms #stacks #strings

Related: [[Stacks - Overview]], [[Stacks - Remove Adjacent Duplicates Example]]
