# What is an Algorithm

An algorithm is a recipe for a computer — a step-by-step set of instructions that takes an **input** and produces an **output** (the answer to a question about that input).

## Requirements (LeetCode context)
- **Deterministic** — same input always gives same output, no randomness
- **Correct for any valid input** — must work for *all* inputs in the defined domain, not just the ones you tested

## Example
Problem: given a non-empty array of positive integers `nums`, find the largest number.

1. Create `maxNum`, initialize to 0
2. Iterate over each `num` in `nums`
3. If `num > maxNum`, update `maxNum = num`
4. Output `maxNum`

⚠️ Edge case bug: initializing `maxNum = 0` breaks if `nums` can contain negatives (they'd never beat 0). Fix: initialize `maxNum = nums[0]` instead.

#dsa #algorithms

Related: [[Big O - Overview]]
