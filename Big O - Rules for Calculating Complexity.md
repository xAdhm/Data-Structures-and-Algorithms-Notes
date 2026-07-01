# Rules for Calculating Big O

## Rule 1 — Ignore constants
O(9999999n) = O(8n) = O(n) = O(n/500)

Why: constants don't change the *growth trend*. If algorithm A does `n` ops and algorithm B does `5n` ops, doubling `n` doubles the work for **both** — they scale identically, even though B is 5x slower in absolute terms. That scaling behavior is what Big O captures, not the raw speed.

## Rule 2 — Only the dominant term survives (as n → ∞)
When adding/subtracting terms of the same variable, drop everything except the fastest-growing term.

O(2ⁿ + n² − 500n) = O(2ⁿ)

Why: as `n → ∞`, the dominant term dwarfs the others into irrelevance. This also means low-order terms like `+500` in `O(n + 500)` just become `O(n)` — they only matter when `n` is small, which isn't the regime Big O analyzes.

## Best possible complexity
`O(1)` = constant time/space — resource usage is the same regardless of input size. Note: `O(1)` doesn't mean *fast*, just *input-independent* (e.g. `O(5,000,000) = O(1)`).

#dsa #algorithms #big-o

Related: [[Big O - Overview]]
