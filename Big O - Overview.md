# Big O Notation

Big O describes the **computational complexity** of an algorithm — how its resource usage scales with input size. Two flavors:

- **Time complexity** — how much longer the algorithm takes as input grows
- **Space complexity** — how much more memory it uses as input grows

Time complexity is usually the one people care about more, but both matter.

## Variables
The variable in the complexity function represents something that changes between inputs and affects the algorithm — usually `n` = length of the input array/string. `n` is just convention, not a rule. You (the programmer) define what the variable represents.

- Multiple inputs → multiple variables, e.g. `O(n·m)` where `n` and `m` are lengths of two different arrays.
- We ignore the cost of individual integer operations (add/multiply/print) growing with integer size — treat all ints as O(1).

## Common complexities
- `O(1)` — constant
- `O(log n)` — logarithmic
- `O(n)` — linear
- `O(n log n)` — linearithmic (efficient sorting)
- `O(n²)` — quadratic
- `O(2ⁿ)` — exponential

## Best / Average / Worst case
Most algorithms have these three cases equal, but not always. If forced to pick one to describe an algorithm: **use worst case**. Never lead with best case.

#dsa #algorithms #big-o

Related: [[Big O - Rules for Calculating Complexity]], [[Time Complexity - Examples]], [[Space Complexity - Examples]]
