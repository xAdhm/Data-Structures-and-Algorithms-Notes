# Hashing - Hash Functions

A **hash function** deterministically converts an input (called a **key**) into an integer smaller than some fixed size chosen by the programmer. Same input → always the same output integer.

## Example (illustrative, not a good hash function)
For a string of English letters:
1. Declare integer `total`
2. For each character, convert it to its alphabet position (a→1, c→3, z→26)
3. Multiply that value by the character's position in the string (index + 1), add to `total`. E.g. in `"abc"`, `b` is alphabet position 2 and string position 2 → contributes `2 * 2 = 4` to `total`
4. After processing all characters, `total % x` is the converted value, where `x` is the fixed size limit

`%` (modulo) is what keeps the result bounded within `[0, x - 1]` — without it, `total` could be arbitrarily large, defeating the "fixed size" requirement.

## The point of a hash function
Arrays offer O(1) random access, but require **integer indices within a fixed range**. A hash function removes that constraint by converting *any* input into a bounded integer — combining a hash function with an array creates a **hash map** (see [[Hashing - Hash Maps]]).

Implementation detail note: this topic (like [[Data Structures - Interface vs Implementation]]) is included mostly for completeness — understanding the *interface* of hash maps/sets matters far more for interviews than memorizing hash function internals.

#dsa #algorithms #hashing

Related: [[Hashing - Hash Maps]], [[Data Structures - Interface vs Implementation]]
