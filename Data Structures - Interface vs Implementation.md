# Data Structures - Interface vs Implementation

A data structure is a format for organizing data efficiently. Practically, it splits into two parts:

## Interface
The "contract" for how to interact with the data structure — what operations exist, what inputs they take, what outputs to expect. This is **how you use it**.

Example (dynamic array): append, insertion, removal, updating, etc. — e.g. `.append()`/`.push()` takes the element to add and typically returns nothing.

## Implementation
The actual code that makes the data structure work under the hood — how data is stored, how operations are carried out internally. Example: a dynamic array's implementation handles memory allocation, size tracking, and shifting elements when removing.

## Why this distinction matters for interviews
Implementation details can get intricate, but for LeetCode/interview purposes, you generally **don't need to memorize them** — they're included in courses mostly for completeness. What actually matters is knowing the **interface**: every major language has built-in implementations of major data structures, and interviews expect you to know how to *use* them, not re-implement them from scratch.

This framing applies directly to [[Hashing - Hash Maps]] and [[Hashing - Sets]], covered next.

#dsa #algorithms #data-structures #hashing
