# Binary Trees - Largest Value in Each Row Example

## Problem: 515. Find Largest Value in Each Tree Row
Given the root of a binary tree, return an array of the largest value in each row (row = level).

## Approach
Same [[Binary Trees - BFS Overview|BFS]] template as [[Binary Trees - Right Side View Example]] — each `while` loop iteration represents one level. Track a `currMax` variable, updated as each node in the current level is processed.

**Efficiency note:** you *could* iterate over the queue first to find the max, then separately process nodes/enqueue children — but it's more efficient to do both in the **same** pass: initialize `currMax` at the start of each level's iteration, then update it inline as each node is dequeued and its children enqueued. By the end of the inner `for` loop, `currMax` holds the correct answer for that level.

Initializing `currMax` fresh at the start of each `while` iteration is what keeps levels handled **separately** — nothing carries over between levels.

## Code
```python
class Solution:
    def largestValues(self, root: Optional[TreeNode]) -> List[int]:
        if not root:
            return []

        ans = []
        queue = deque([root])

        while queue:
            current_length = len(queue)
            curr_max = float("-inf") # this will store the largest value for the current level

            for _ in range(current_length):
                node = queue.popleft()
                curr_max = max(curr_max, node.val)
                if node.left:
                    queue.append(node.left)
                if node.right:
                    queue.append(node.right)

            ans.append(curr_max)

        return ans
```

## Complexity
**O(n) time and O(n) space** — identical reasoning to [[Binary Trees - Right Side View Example]] and the general [[Binary Trees - BFS Overview|BFS]] template.

## Takeaway
Notice how similar this code is to the Right Side View example — same overall shape (BFS template + one running value per level), just tracking a different quantity (`max` instead of "last node seen"). This is a common theme: once you recognize the level-by-level BFS pattern, adapting it to track different per-level values is usually a small tweak, not a rewrite.

#dsa #algorithms #trees #binary-trees #queues

Related: [[Binary Trees - BFS Overview]], [[Binary Trees - Right Side View Example]]
