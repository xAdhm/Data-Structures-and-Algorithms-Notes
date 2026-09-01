# Complexity Cheatsheet - By Data Structure

Reference table of time complexities for common operations, organized by data structure. Companion to [[Big O - Overview]] and the individual data structure notes.

## Arrays (dynamic array/list)
`n = arr.length`
- Add/remove at the end: **O(1) amortized**
- Add/remove at arbitrary index: **O(n)**
- Access/modify at arbitrary index: **O(1)**
- Check if element exists: **O(n)**
- [[Two Pointers - Overview|Two pointers]]: **O(n·k)**, `k` = work per iteration (includes [[Sliding Window - Overview|sliding window]])
- Building a [[Prefix Sum - Overview|prefix sum]]: **O(n)**
- Finding a subarray sum given a prefix sum: **O(1)**

## Strings (immutable)
`n = s.length`
- Add/remove character: **O(n)**
- Access at arbitrary index: **O(1)**
- Concatenation between two strings: **O(n + m)**, `m` = other string's length
- Create substring: **O(m)**, `m` = substring length
- Two pointers: **O(n·k)**
- [[String Building - O(n) Technique|Building a string]] from an array/join/StringBuilder: **O(n)**

## Linked Lists
`n` = number of nodes
- Add/remove given a pointer **before** the location: **O(1)**
- Add/remove given a pointer **at** the location: **O(1)** if [[Linked Lists - Doubly Linked List|doubly linked]]
- Add/remove at arbitrary position **without** a pointer: **O(n)**
- Access at arbitrary position without a pointer: **O(n)**
- Check if element exists: **O(n)**
- Reverse between positions `i` and `j`: **O(j - i)**
- Detect a cycle: **O(n)** (via [[Fast and Slow Pointers - Cycle Detection|fast-slow pointers]] or a hash map)

## Hash table / dictionary
`n = dic.length`
- Add/remove key-value pair: **O(1)**
- Check if key exists: **O(1)**
- Check if value exists: **O(n)**
- Access/modify value by key: **O(1)**
- Iterate over keys/values/both: **O(n)**

**Caveat:** O(1) operations are constant *relative to `n`* — hashing itself can cost more. E.g. string keys cost O(m) to hash, where `m` = string length (see [[Hashing - Hash Maps vs Arrays]]).

## Set
`n = set.length`
- Add/remove element: **O(1)**
- Check if element exists: **O(1)**
(Same hashing caveat as hash tables applies.)

## Stack
Depends on implementation; if backed by a dynamic array (`n = stack.length`):
- Push: **O(1)**
- Pop: **O(1)**
- Peek: **O(1)**
- Access/modify at arbitrary index: **O(1)**
- Check if element exists: **O(n)**

## Queue
Depends on implementation; if backed by a doubly linked list (`n = queue.length`):
- Enqueue: **O(1)**
- Dequeue: **O(1)**
- Peek: **O(1)**
- Access/modify at arbitrary index: **O(n)**
- Check if element exists: **O(n)**

**Note:** most languages implement queues more sophisticatedly than a plain doubly linked list — indexed access may be faster than O(n), or still O(n) but with a much smaller constant.

## Binary tree problems (DFS/BFS)
`n` = number of nodes. Most algorithms run in **O(n·k)**, `k` = work per node (usually O(1)) — assumes an efficient queue for BFS. General rule, not universal.

## Binary search tree
`n` = number of nodes
- Add/remove: **O(n) worst case, O(log n) average**
- Check if element exists: **O(n) worst case, O(log n) average**

Average case = well-balanced tree (each depth close to full). Worst case = the tree degenerates into a straight line.

## Heap / priority queue
`n = heap.length` (min heap):
- Add: **O(log n)**
- Delete the minimum: **O(log n)**
- Find the minimum: **O(1)**
- Check if element exists: **O(n)**

## Binary search
**O(log n)** worst case, `n` = initial search space size.

## Miscellaneous
- Sorting: **O(n log n)**, `n` = size of data sorted
- Graph DFS/BFS: **O(n·k + e)**, `n` = nodes, `e` = edges, `k` = work per node (excluding edge iteration)
- Graph DFS/BFS space: typically O(n), or O(n + e) if the graph itself needs to be stored
- [[Dynamic Programming - Complexity|DP time complexity]]: **O(n·k)**, `n` = number of states, `k` = work per state
- DP space complexity: **O(n)**, `n` = number of states

#dsa #algorithms #big-o #reference

Related: [[Big O - Overview]], [[Complexity Cheatsheet - Input Size Guide]]
