# Hashing - Hash Maps

A **hash map** (aka hash table or dictionary) combines a [[Hashing - Hash Functions|hash function]] with an array. Where arrays map *indices* to values, hash maps map **keys** to values — and a key can be almost anything (typical constraint: keys must be **immutable**; values can be anything).

Python example: `dic = {}`

## Why it matters
Arguably the single most important concept in algorithm interviewing — hash maps can reduce an algorithm's time complexity by a factor of **O(n)** across a huge range of problems. Every major language has a built-in implementation.

## Core properties
- **Unordered**: no guarantee on iteration order (implementation/language dependent). Contrast with an **ordered** data structure, where insertion order is remembered.
- Stores **key-value pairs**
- All O(1):
  - Add an element (associate a key with a value)
  - Delete an element if it exists
  - Check if a key exists
  - Update the value for a key
  - Find the length / number of elements
- Can iterate over keys and/or values, but without guaranteed order

See [[Hashing - Hash Maps vs Arrays]] for a full complexity/tradeoff comparison, and [[Hashing - Sets]] for the related "keys-only" structure.

#dsa #algorithms #hashing #hash-map

Related: [[Hashing - Hash Functions]], [[Hashing - Hash Maps vs Arrays]], [[Hashing - Sets]], [[Hashing - Arrays as Keys]]
