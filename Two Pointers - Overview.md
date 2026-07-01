# Two Pointers - Overview

Two pointers is a very common technique for solving array and string problems. It involves two integer variables (commonly `i`/`j` or `left`/`right`) that each represent an index, moving along an iterable (array or string) according to some logic.

It's not one fixed algorithm — it's an abstract idea ("use two index variables that move along iterables") that can be implemented in different ways depending on the problem. See:
- [[Two Pointers - Converging Pointers Method]] — pointers start at opposite ends and move toward each other (single iterable)
- [[Two Pointers - Two Iterables Method]] — pointers move forward simultaneously across two separate iterables

## Why it's powerful
If the work done per iteration is O(1), two pointers techniques typically achieve **O(n) time** and **O(1) space** — often replacing a brute-force O(n²) approach. This is because each pointer can only move a bounded number of times (at most n total steps), so the loop can't run more than O(n) iterations.

## Closing notes / flexibility
- The patterns shown in the related notes are guidelines, not rigid rules. Pointers don't have to start at the first/last index — sometimes a problem calls for different starting points.
- The "two iterables" method can also apply to a *single* array/string if the problem calls for two pointers moving independently over the same input.
- There are even problems that use **three pointers** — the core idea (multiple index variables moving along iterables) generalizes.
- Two pointers shows up constantly in later topics — this isn't the last time it's covered.

#dsa #algorithms #two-pointers #arrays #strings
