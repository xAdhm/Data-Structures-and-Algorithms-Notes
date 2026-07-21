# Queues - Overview

Where a [[Stacks - Overview|stack]] follows LIFO, a **queue** follows **FIFO** — First In, First Out. Elements are added and removed from **opposite** ends (contrast with a stack, where both happen on the same end).

Physical analogy: a line at a fast food restaurant — people join at the back, leave from the front, and the first people in line are the first to leave. Software analogy: any first-come-first-served job system (e.g. multiple print jobs queued for one printer).

## Terminology
- **Enqueue** — add an element (to the back)
- **Dequeue** — remove an element (from the front)

## Implementation
Like a stack, a queue is an **abstract interface** — what matters is adding/removing from opposite ends, not the specific implementation.

**The catch:** a plain dynamic array works fine for a stack, but front-of-array operations (add/remove) cost **O(n)** on a dynamic array (see [[Arrays and Strings - Time Complexity of Operations]]) — bad for a queue, since dequeuing is a front operation.

**Efficient implementation: doubly linked list.** With a [[Linked Lists - Doubly Linked List|doubly linked list]] that maintains pointers to both head and tail (typically with [[Linked Lists - Sentinel Nodes|sentinel nodes]]), you get **O(1)** add/remove at either end — since having a direct pointer to the node at a position makes doubly linked list operations O(1).

## Deque (double-ended queue)
A **deque** ("deck") allows adding/removing from **both** ends. A regular queue restricts you to enqueue-at-one-end, dequeue-at-the-other; a deque relaxes that restriction entirely.

## Python interface
```python
# Declaration: we will use deque from the collections module
import collections
queue = collections.deque()

# If you want to initialize it with some initial values:
queue = collections.deque([1, 2, 3])

# Enqueueing/adding elements:
queue.append(4)
queue.append(5)

# Dequeuing/removing elements:
queue.popleft()   # 1
queue.popleft()   # 2

# Check element at front of queue (next element to be removed)
queue[0]          # 3

# Get size
len(queue)        # 3
```

## Where queues actually come up
Queues are less common in algorithm problems than stacks, and problems tend to be more difficult. The **main use case** is implementing **breadth-first search (BFS)** — covered in a later trees & graphs chapter. Outside of BFS, few problems center specifically on a queue — but see [[Queues - Recent Calls Example]] for one that does.

The **monotonic** pattern (a later chapter) applies to both stacks and queues, and includes a few more queue-based examples.

#dsa #algorithms #queues

Related: [[Stacks - Overview]], [[Linked Lists - Doubly Linked List]], [[Linked Lists - Sentinel Nodes]], [[Queues - Recent Calls Example]]
