# Stacks - Valid Parentheses Example

## Problem: 20. Valid Parentheses
Given a string `s` containing only `'(' ')' '{' '}' '[' ']'`, determine if it's valid — every open bracket must be closed by the matching type, in the correct order, with each closing bracket closing exactly one open bracket.

Example: `"({})"` and `"(){}[]"` are valid; `"(]"` and `"({)}"` are not.

## Recognizing the LIFO pattern
The "correct order" is defined relative to the **most recent unclosed opening bracket** — a closing bracket must match whichever opening bracket appeared most recently and hasn't been closed yet. This is exactly **LIFO**: the last opening bracket seen is the first one that needs to be closed. That's the signal to reach for [[Stacks - Overview|a stack]].

## Approach
- Iterate over the string.
- **Opening bracket** → push it onto the stack.
- **Closing bracket** → pop the stack (the most recent unmatched opening bracket) and check it matches:
  - If the stack was empty when we needed to pop → invalid (no opening bracket available, e.g. `"{}]"`)
  - If the popped opening bracket doesn't correspond to the current closing bracket → invalid
- At the end, the stack must be **empty** — any remaining unclosed opening brackets (e.g. `"(){"`) means the string is invalid.

**Matching brackets:** use a hash map from opening bracket → its corresponding closing bracket, so checking a match is an O(1) lookup (see [[Hashing - Hash Maps]]).

## Code
```python
class Solution:
    def isValid(self, s: str) -> bool:
        stack = []
        matching = {"(": ")", "[": "]", "{": "}"}

        for c in s:
            if c in matching: # if c is an opening bracket
                stack.append(c)
            else:
                if not stack:
                    return False

                previous_opening = stack.pop()
                if matching[previous_opening] != c:
                    return False

        return not stack
```

## Complexity
**O(n) time** — each character is pushed or popped at most once, and stack operations are O(1) (see [[Stacks - Overview]]). **O(n) space** — the stack can grow linearly with unmatched opening brackets.

#dsa #algorithms #stacks #strings

Related: [[Stacks - Overview]], [[Hashing - Hash Maps]]
