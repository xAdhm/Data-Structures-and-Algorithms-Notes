# Hashing - Sets

A **set** uses the same hashing mechanism as a [[Hashing - Hash Maps|hash map]], but doesn't map keys to values — it only tracks whether a key exists. Basically: "a hash map if you only consider the keys."

## Operations — all O(1)
- Add an element
- Remove an element
- Check if an element exists

## Key property: no frequency tracking
Adding the same element to a set multiple times has no additional effect after the first — e.g. adding the same value 100 times: the first call adds it, the other 99 do nothing. A set doesn't know or care *how many times* something was added, only *whether* it currently exists.

Sets are the natural choice whenever a problem only cares about **existence checks**, not associated values or counts.

#dsa #algorithms #hashing #sets

Related: [[Hashing - Hash Maps]], [[Hashing - Hash Functions]]
