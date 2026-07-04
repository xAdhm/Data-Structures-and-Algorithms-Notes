# Hashing - Hash Maps vs Arrays

## Where hash maps win
These are all O(1) for a hash map (see [[Hashing - Hash Maps]]), versus O(n) for an unsorted array:
- Add an element and associate it with a value
- Delete an element if it exists
- Check if an element exists

Hash maps also match arrays' O(1) performance on:
- Find length / number of elements
- Updating values
- Iterating over elements

Hash maps are also more convenient in practice: if you don't know the maximum size your keys could take, you'd need to guess an array size — with a hash map, that's a non-issue, since keys get converted into a bounded integer via the hash function regardless.

## Where arrays win — practical tradeoffs (good interview talking points)

**1. Overhead on small inputs.** Big O ignores constants (see [[Big O - Rules for Calculating Complexity]]), so hash map "O(1)" is often more like "O(10)" in practice — every key has to pass through the hash function. For small inputs, a plain array can be faster.

**2. Space usage / resizing cost.** Both dynamic arrays and hash tables are implemented as fixed-size arrays that resize when capacity is exceeded — but:
- Resizing a hash table is more expensive: every existing key must be **re-hashed**
- A hash table's underlying array may be sized much larger than the actual number of stored elements (e.g. capacity for 10,000 but only storing 10) → wasted space
- When you don't know how many elements you'll need to store, arrays are more flexible/space-efficient about resizing

## A subtlety about "O(1)"
Time complexity only concerns the variables you define. Hash map operations are O(1) with respect to `n` (the size of the map) — but this can be misleading. E.g. hashing a string key costs **O(m)**, where `m` is the length of that string. The "constant time" claim is only constant *relative to the map's size* — not necessarily relative to the size of individual keys.

#dsa #algorithms #hashing #hash-map #big-o

Related: [[Hashing - Hash Maps]], [[Big O - Rules for Calculating Complexity]], [[Arrays and Strings - Time Complexity of Operations]]
