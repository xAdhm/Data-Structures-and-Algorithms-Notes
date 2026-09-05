# Modular Arithmetic - Overview

Rarely needed in an interview, but a simple concept worth knowing — more relevant to competitive programming and a handful of LeetCode problems.

## The problem it solves
Some problems ask for an answer **mod x** (on LeetCode, typically `x = 10^9 + 7`), because the true answer could be astronomically large — too big to store or compute efficiently. The naive approach (compute the full massive answer, then `% MOD` at the very end) is technically correct, but **inefficient**: arithmetic on extremely large numbers isn't free — cost grows with the number of digits involved.

## The key property: modulo can be applied at every step
Taking the modulus **after every operation**, not just at the end, produces the **same final answer** — for both products and sums.

**Worked example:** `MOD = 7`, sequence `[11, 15, 26, 43, 62]`.
- **Full computation:** product = `11,437,140`, `% 7 = 1`. Sum = `157`, `% 7 = 3`.
- **Mod at every step (product):** `11*15=165 → %7=4`; `4*26=104 → %7=6`; `6*43=258 → %7=6`; `6*62=372 → %7=1`. Same final answer: `1`.
- **Mod at every step (sum):** `11+15=26 → %7=5`; `5+26=31 → %7=3`; `3+43=46 → %7=4`; `4+62=66 → %7=3`. Same final answer: `3`.

The result is identical **no matter how early you stop** or how many more numbers get added — this holds generally, not just for this example.

## Why this matters practically
Applying modulo at each step keeps every intermediate value small (bounded by `MOD`), avoiding ever computing with massive numbers. For huge inputs (e.g. a million integers), the "true" product could reach absurd magnitudes (e.g. `10^(1,000,000,000)`). In a language without overflow (like Python), multiplying numbers in the range `0` to `MOD-1` repeatedly is far faster than multiplying numbers with a billion digits. In a language *with* overflow (fixed-size integers), keeping numbers small isn't just faster — it's **necessary** to avoid incorrect results entirely.

## When to think about this
On LeetCode: whenever the problem explicitly gives a modulus in the description. More generally: any time a problem (or even a system design discussion) could produce potentially massive numbers.

See [[Modular Arithmetic - Maximum Product After K Increments Example]] and [[Modular Arithmetic - Divisibility Array Example]] for worked applications.

#dsa #algorithms #modular-arithmetic

Related: [[Modular Arithmetic - Maximum Product After K Increments Example]], [[Modular Arithmetic - Divisibility Array Example]]
