# Binary Search Trees - Minimum Absolute Difference Example

## Problem: 530. Minimum Absolute Difference in BST
Given the root of a BST, return the minimum absolute difference between any two different node values.

## Building up to the optimal approach
- **Brute force:** collect all values, check every pair → **O(n²)**.
- **Better:** sort the collected values, then only check **adjacent** elements — the minimum difference must occur between adjacent elements in sorted order (any non-adjacent pair has an adjacent pair with an equal-or-smaller gap between them). This gets to **O(n log n)**, dominated by the sort.
- **Best:** skip the sort entirely by using the [[Binary Search Trees - Overview|BST inorder-traversal-gives-sorted-order]] trick — an inorder DFS naturally produces sorted values in **O(n)**, no sorting needed.

## Recursive code
```python
class Solution:
    def getMinimumDifference(self, root: Optional[TreeNode]) -> int:
        def dfs(node):
            if not node:
                return

            left = dfs(node.left)
            values.append(node.val)
            right = dfs(node.right)

        values = []
        dfs(root)
        ans = float("inf")
        for i in range(1, len(values)):
            ans = min(ans, values[i] - values[i - 1])

        return ans
```
`dfs` is a pure inorder traversal — calls left, then appends the current value, then calls right — so `values` fills up in sorted order. Once populated, only adjacent differences need checking.

## Iterative code
```python
class Solution:
    def getMinimumDifference(self, root: Optional[TreeNode]) -> int:
        def iterative_inorder(root):
            stack = []
            values = []
            curr = root
            while stack or curr:
                if curr:
                    stack.append(curr)
                    curr = curr.left
                else:
                    curr = stack.pop()
                    values.append(curr.val)
                    curr = curr.right

            return values

        values = iterative_inorder(root)
        ans = float("inf")
        for i in range(1, len(values)):
            ans = min(ans, values[i] - values[i - 1])

        return ans
```

**Note on iterative inorder complexity:** as mentioned in [[Binary Trees - Iterative DFS]], preorder is easy to implement iteratively, but inorder (and postorder) are meaningfully more complex — this iterative inorder helper demonstrates that added complexity directly. Prefer the recursive version when given the choice; the iterative version is mainly worth knowing in case an interviewer specifically asks for it.

## Complexity
**O(n) time, O(n) space** — linear traversal to collect sorted values (no sort needed), plus a linear scan for adjacent differences.

#dsa #algorithms #trees #binary-search-trees #recursion

Related: [[Binary Search Trees - Overview]], [[Binary Trees - Iterative DFS]]
