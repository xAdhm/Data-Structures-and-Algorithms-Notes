# Stacks - Overview

A **stack** is an ordered collection where elements are only added and removed from the **same end**.

Physical analogy: a stack of plates — you add and remove from the top only. Software analogy: browser tab history — visiting site A, then B, then C gives history `[A, B, C]`. Clicking "back" removes from the same end you were adding to: click once → `[A, B]`, again → `[A]`.

## LIFO
Stacks are described as **LIFO** — Last In, First Out. The most recently added element is always the first one removed.

## Terminology
- **Push** — insert an element (onto the top)
- **Pop** — remove an element (from the top)
- **Peek** — look at the top element without removing it

## Implementation
A stack is an **abstract interface** — what matters is that add/remove happen from the same end, not the underlying implementation. Some languages have built-in stack types (e.g. Java). In Python, a plain list works directly: `stack = []`, `stack.append(x)` to push, `stack.pop()` to pop. Any dynamic array can implement a stack. A stack can also be implemented with a linked list using a tail pointer.

## Time complexity (array-backed implementation)
Since a list/dynamic array is the most common backing structure, stack operations inherit array time complexity (see [[Arrays and Strings - Time Complexity of Operations]]):
- Push, pop, random access: **O(1)**
- Search: **O(n)**

## Stacks and recursion
Stacks and recursion are deeply related — recursion is *literally implemented* using a call stack under the hood. Each function call gets pushed onto the stack; the call at the top is the currently "active" one; when a call returns (or the function ends), it's popped off. This connects directly to how [[Recursion - Call Stack and Execution Order]] explained execution order — that entire explanation was describing a stack in action.

## When to reach for a stack in algorithm problems
Look for the **LIFO pattern** — usually some interaction between elements in the input:
- Matching elements together
- Querying a property like "how far is the next largest element"
- Evaluating a math expression given as a string
- Comparing elements against each other in some order-dependent way

The LIFO nature isn't always obvious at first glance — recognizing it is a skill built through examples (covered in the rest of this chapter).

## Python interface
```python
# Declaration: we will just use a list
stack = []

# Pushing elements:
stack.append(1)
stack.append(2)
stack.append(3)

# Popping elements:
stack.pop()   # 3
stack.pop()   # 2

# Check if empty
not stack     # False

# Check element at top
stack[-1]     # 1

# Get size
len(stack)    # 1
```

#dsa #algorithms #stacks

Related: [[Recursion - Call Stack and Execution Order]], [[Arrays and Strings - Time Complexity of Operations]]
