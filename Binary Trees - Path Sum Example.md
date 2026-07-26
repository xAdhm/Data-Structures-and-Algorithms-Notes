# Binary Trees - Path Sum Example

## Problem: 112. Path Sum
Given the root of a binary tree and integer `targetSum`, return true if a root-to-leaf path exists whose node values sum to `targetSum`.

## What extra state does each call need?
Beyond the current node, we need to track the **running sum** from the root down to the current node — call it `curr`. Define a helper `dfs(node, curr)` that returns true if a path exists from `node` to some leaf, summing to `targetSum`, given that `curr` has already been accumulated so far.

## Key structural observation
**Every path from the root through a child of `node` must pass through `node` itself.** This is why it's always safe to do `curr += node.val` at the current node before recursing — every call's own `curr` value stays accurate to that call's specific path, thanks to each recursive call having independent local variables (same idea used in [[Binary Trees - Maximum Depth Example]]).

## Base cases
- Empty tree (`node` is `None`) → no path possible → `False`
- Leaf node (both children `None`) → check `(curr + node.val) == targetSum` directly

## Combining subtree results
Not a leaf → try both children, return true if **either** works (`or`) — the problem only needs *some* valid path to exist, not all of them.

## Recursive code
```python
class Solution:
    def hasPathSum(self, root: Optional[TreeNode], targetSum: int) -> bool:
        def dfs(node, curr):
            if not node:
                return False

            # if both children are null, then the node is a leaf
            if node.left == None and node.right == None:
                return (curr + node.val) == targetSum

            curr += node.val
            left = dfs(node.left, curr)
            right = dfs(node.right, curr)
            return left or right

        return dfs(root, 0)
```

Because the function uses `or`, a single `True` found anywhere in the tree propagates all the way back up to the original root call.

## Iterative code
```python
class Solution:
    def hasPathSum(self, root: Optional[TreeNode], targetSum: int) -> bool:
        if not root:
            return False
        stack = [(root, 0)]
        while stack:
            node, curr = stack.pop()
            # if both children are null, then the node is a leaf
            if node.left == None and node.right == None:
                if (curr + node.val) == targetSum:
                    return True
            curr += node.val
            if node.left:
                stack.append((node.left, curr))
            if node.right:
                stack.append((node.right, curr))
        return False
```
(Iterative is much less common in practice — mainly useful if specifically requested in an interview; see [[Binary Trees - Iterative DFS]].)

## Complexity
**O(n) time, O(n) space** worst case (straight-line tree, per [[Binary Trees - Iterative DFS]]) — each node visited at most once, constant work per visit.

#dsa #algorithms #trees #binary-trees #recursion

Related: [[Binary Trees - Maximum Depth Example]], [[Binary Trees - Count Good Nodes Example]]
