# Arrays and Strings - Time Complexity of Operations

Quick reference for the time complexity of common array/string operations (arrays assumed dynamic/list-like, strings assumed immutable — see [[Arrays and Strings - Overview]]).

| Operation | Array / List | String (Immutable) |
|---|---|---|
| Appending to end | *O(1) | O(n) |
| Popping from end | O(1) | O(n) |
| Insertion, not from end | O(n) | O(n) |
| Deletion, not from end | O(n) | O(n) |
| Modifying an element | O(1) | O(n) |
| Random access | O(1) | O(1) |
| Checking if element exists | O(n) | O(n) |

## Notes
- **\*Appending to end of an array/list is amortized O(1).** "Amortized" means: any *single* append could occasionally cost more (e.g. when the underlying array needs to resize/reallocate), but the *average* cost per append across many operations works out to O(1) — the occasional expensive resize gets "spread out" over all the cheap O(1) appends.
- **Strings are O(n) for almost everything except random access**, because they're immutable — any modification (append, pop, insert, delete, modify a single char) requires rebuilding the whole string. Random access (reading a character by index) is still O(1) since no rebuild is needed to just *read*.
- **Arrays are O(n) for insertion/deletion in the middle**, because all subsequent elements need to shift over by one position. Only end operations (append/pop) avoid this shift.
- **Checking if an element exists is O(n) for both** — without extra structure (like a hash set), you have to scan linearly in the worst case.

#dsa #algorithms #arrays #strings #big-o

Related: [[Arrays and Strings - Overview]], [[Big O - Overview]]
