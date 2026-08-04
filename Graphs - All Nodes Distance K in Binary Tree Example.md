# Graphs - All Nodes Distance K in Binary Tree Example

## Problem: 863. All Nodes Distance K in Binary Tree
Given the root of a binary tree, a `target` node, and integer `k`, return the values of all nodes at distance `k` from `target`.

## The core obstacle
[[Binary Trees - Overview|Binary trees]] only have parent → child pointers — no way to move back up. Finding nodes at distance `k` *within* `target`'s own subtree is straightforward, but nodes elsewhere in the tree (reachable only by going up through `target`'s ancestors) are normally unreachable.

## The fix: convert the tree into an undirected graph
Perform a preliminary [[Binary Trees - DFS Overview|DFS]] from the root, assigning every node a `.parent` pointer (order doesn't matter for this part — DFS or BFS both work). Once every node knows its parent *and* its children, the tree effectively becomes navigable in **all directions** — i.e., an undirected graph — and [[Graphs - BFS Overview|BFS]] can be used to find nodes at an exact distance.

**Implementation note:** Python/JavaScript can assign a `.parent` attribute directly onto node objects; Java/C++ typically use a hash map instead (mapping node → parent) since directly mutating objects with new attributes isn't idiomatic there. Even in Python, be cautious about this practice in an interview — a hash map may be viewed as the "safer," more broadly acceptable approach.

## Approach
1. DFS from the root, assigning `.parent` to every node.
2. BFS starting from `target` (not the root!) — since we now have parent pointers, `target`'s "neighbors" are `node.left`, `node.right`, **and** `node.parent`.
3. Use the level-based `for`-loop-inside-`while`-loop format (same as [[Binary Trees - BFS Overview|standard tree BFS]]), since this problem *does* care about a whole level as a group — specifically, the level that's exactly `k` steps away.
4. After exactly `k` iterations of the `while` loop, the queue holds precisely the nodes at distance `k` from `target`.

## Code
```python
from collections import deque

class Solution:
    def distanceK(self, root: TreeNode, target: TreeNode, k: int) -> List[int]:
        def dfs(node, parent):
            if not node:
                return

            node.parent = parent
            dfs(node.left, node)
            dfs(node.right, node)

        dfs(root, None)
        queue = deque([target])
        seen = {target}
        distance = 0

        while queue and distance < k:
            current_length = len(queue)
            for _ in range(current_length):
                node = queue.popleft()
                for neighbor in [node.left, node.right, node.parent]:
                    if neighbor and neighbor not in seen:
                        seen.add(neighbor)
                        queue.append(neighbor)

            distance += 1

        return [node.val for node in queue]
```

**Why the `while` loop condition checks `distance < k`:** the loop stops exactly when `k` levels have been processed — at that point, the queue holds exactly the answer, with no need to process further levels.

## Complexity
**O(n) time, O(n) space** — both the parent-assignment DFS and the BFS visit each node at most once with constant work per node. Space comes from the DFS recursion call stack, the queue, and `seen`.

#dsa #algorithms #graphs #trees #binary-trees

Related: [[Graphs - BFS Overview]], [[Binary Trees - BFS Overview]], [[Binary Trees - DFS Overview]]
