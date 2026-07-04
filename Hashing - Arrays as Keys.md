# Hashing - Arrays as Keys

Hash map keys generally must be **immutable** (see [[Hashing - Hash Maps]]) — but arrays are mutable. So how do you use an array (or its contents) as a key?

## Common tricks
- **Convert to an immutable type**, if your language has one:
  - Python: tuples are immutable → `tuple(arr)` works directly as a key
- **Convert to a delimited string**, using a separator guaranteed not to appear in any element:
  - E.g. comma-separated integers: `[1, 51, 163]` → `"1,51,163"`

## Language-specific alternatives
Some languages offer data structures that allow mutable-structure-like keys — e.g. C++'s `std::map`. Important distinction: **these are not hash maps** (they're typically implemented differently, often as balanced trees, with different complexity guarantees), but they can solve similar problems where you need array-like or mutable keys.

#dsa #algorithms #hashing #hash-map

Related: [[Hashing - Hash Maps]], [[Data Structures - Interface vs Implementation]]
