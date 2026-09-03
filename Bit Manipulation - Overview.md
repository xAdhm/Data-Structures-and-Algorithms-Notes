# Bit Manipulation - Overview

Bit manipulation looks at data in binary form and manipulates individual "bits" — can improve algorithm complexity in clever ways.

## Core operations
- **OR (`|`):** result bit is `1` if **any** input bit is `1`.
- **AND (`&`):** result bit is `1` only if **all** input bits are `1`.
- **XOR (`^`):** result bit is `1` if the number of `1` bits is **odd**.
- **Left/right shift (`<<`, `>>`):** shifts every bit one position in that direction. A right shift "deletes" the bit that falls off the end. Shifting corresponds to multiplying/dividing by 2 — left shift = ×2, right shift = floor division by 2.

These operations apply **bit by bit** across the whole number. Example: `x = 15` (`1111`), `y = 12` (`1100`):
- `x | y = 1111 = 15`
- `x & y = 1100 = 12`
- `x ^ y = 0011 = 3`
- `x << 1 = 11110 = 30`
- `x >> 1 = 111 = 7`

## Bitmasks
A **bitmask** (or just "mask") isolates specific bits for inspection/modification. E.g. to focus only on the 2nd bit (0-indexed from the right, representing decimal `4`): `mask = 1 << 2` → binary `100`.

- **Check if a bit is set:** `mask & x` — non-zero **if and only if** that specific bit is set in `x` (since every other bit in `mask` is `0`, contributing nothing to the AND).
- **Flip a bit:** `mask ^ x` — XOR only affects bits where `mask` has a `1`; everywhere else, XOR-ing with `0` leaves `x` unchanged.

**XOR intuition:** `x XOR 0` leaves `x` unchanged; `x XOR 1` flips `x`.

See [[Bit Manipulation - Single Number Example]] and [[Bit Manipulation - Bitmasks for Visited State]] for worked applications.

#dsa #algorithms #bit-manipulation

Related: [[Bit Manipulation - Single Number Example]], [[Bit Manipulation - Bitmasks for Visited State]]
