# Binary Trees - Right Side View Example

## Problem: 199. Binary Tree Right Side View
Given the root of a binary tree, return the values of the nodes visible when standing on the right side of the tree, top to bottom.

## Reframing the problem
Standing on the right side, you see exactly one node per level — the **rightmost** node of each level. This reduces to: "find the rightmost node at every level" — a natural fit for [[Binary Trees - BFS Overview|BFS]], since each `while` loop iteration already represents processing one full level.

## Why the last element in the queue is the rightmost node
Using the standard BFS template, if children are enqueued **left before right**, the queue at the start of each level naturally holds nodes in left-to-right order. That means the **last element currently in the queue** is always the rightmost node of the current level — no extra tracking needed, just read `queue[-1]` before processing the level.

## Code
```python
class Solution:
    def rightSideView(self, root: Optional[TreeNode]) -> List[int]:
        if not root:
            return []

        ans = []
        queue = deque([root])

        while queue:
            current_length = len(queue)
            ans.append(queue[-1].val) # this is the rightmost node for the current level

            for _ in range(current_length):
                node = queue.popleft()
                if node.left:
                    queue.append(node.left)
                if node.right:
                    queue.append(node.right)

        return ans
```

Note `queue[-1].val` is read **before** the inner loop processes and mutates the queue — at that exact moment, the queue still contains only the current level, in left-to-right order, so its last entry is guaranteed correct.

## Complexity
**O(n) time and O(n) space** — each node visited once, O(1) work per node, queue can hold up to O(n) nodes (widest level, see [[Binary Trees - BFS vs DFS]]).

#dsa #algorithms #trees #binary-trees #queues

Related: [[Binary Trees - BFS Overview]], [[Binary Trees - Largest Value in Each Row Example]]
