# Binary Trees - BFS Overview

Where [[Binary Trees - DFS Overview|DFS]] prioritizes **depth**, **breadth-first search (BFS)** prioritizes **breadth** — visiting all nodes at a given depth before moving to the next depth.

## Visiting order contrast
DFS traversal of a large tree visits depths in a pattern like `0, 1, 2, 3, 4, 5, 6, ...` (going as deep as possible before backtracking). BFS instead visits like `0, 1, 1, 2, 2, 2, 2, 3, 3, ...` — every node at depth `d` gets visited before any node at depth `d + 1`.

## "Level" terminology
Each depth of a tree can be thought of as a **level** — like floors of a building, with the root as the top floor and edges as staircases down. BFS processes the tree level by level, top to bottom.

**Complete binary tree** definition (relevant terminology): every level is full except possibly the last, and the last level's nodes are packed as far left as possible.

## Implementation: queue, not stack
DFS uses a stack (explicitly, or implicitly via the recursive call stack). BFS is implemented **iteratively with a [[Queues - Overview|queue]]** — this course covers only the iterative version, since a recursive BFS implementation is technically possible but considerably more awkward with no real benefit.

## General BFS template
```python
from collections import deque

def print_all_nodes(root):
    queue = deque([root])
    while queue:
        nodes_in_current_level = len(queue)
        # do some logic here for the current level
        for _ in range(nodes_in_current_level):
            node = queue.popleft()

            # do some logic here on the current node
            print(node.val)
            # put the next level onto the queue
            if node.left:
                queue.append(node.left)
            if node.right:
                queue.append(node.right)
```

**How it works:** at the start of each `while` iteration, the queue holds exactly all the nodes of the current level (initially just the root). Recording `nodes_in_current_level` before the inner `for` loop caps that loop to only the current level's nodes — without this, the loop would keep consuming newly-added next-level nodes too. As each node is processed, its children (the *next* level) get enqueued. Because removal happens from the front and insertion happens at the back (opposite ends — the defining trait of a queue), by the time the `for` loop ends, the queue contains exactly the next level's nodes, ready for the next `while` iteration.

## Complexity
Same as [[Binary Trees - Iterative DFS|DFS]]: with an efficient queue, enqueue/dequeue are O(1), so overall time is **O(n·k)** where `n` = total nodes and `k` = work per node (usually O(1), giving **O(n)**). Each node is visited exactly once.

See [[Binary Trees - BFS vs DFS]] for when to choose one over the other, and [[Binary Trees - Right Side View Example]] / [[Binary Trees - Largest Value in Each Row Example]] for worked examples.

#dsa #algorithms #trees #binary-trees #queues

Related: [[Binary Trees - DFS Overview]], [[Queues - Overview]], [[Binary Trees - BFS vs DFS]]
