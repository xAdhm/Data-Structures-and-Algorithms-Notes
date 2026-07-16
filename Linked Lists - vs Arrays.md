# Linked Lists - vs Arrays

Not hugely relevant to solving algorithm problems directly — almost all linked list problems give you the linked list as input, so there's no real "should I use a linked list" decision to make. Still useful for interview trivia/discussion, and a few problems do use a linked list as part of the optimal solution.

## Advantage: O(1) insertion/removal at any position
...**but only if you already have a reference** to the node at that position. Without one, you must iterate from the head to reach it first, making the operation **O(n)**. Still, this beats a dynamic array, which always needs O(n) to insert/remove from an arbitrary position (see [[Arrays and Strings - Time Complexity of Operations]]).

## Disadvantage: no random access
Arrays offer O(1) indexing; linked lists don't. To reach the 150,000th element, you generally have no better option than starting at the head and iterating 150,000 times → **O(n)** access.

## Other notes (less relevant to algorithm problems, more for interview discussion)
- **No fixed size:** dynamic arrays resize when capacity is exceeded (an expensive operation) — linked lists don't have this issue since nodes are allocated individually.
- **More overhead:** every linked list node needs extra storage for pointer(s). If storing small items (booleans, characters), this overhead could more than double the space needed compared to a plain array.

#dsa #algorithms #linked-lists #big-o

Related: [[Linked Lists - Overview]], [[Arrays and Strings - Time Complexity of Operations]]
