# Binary Trees - Same Tree Example

## Problem: 100. Same Tree
Given the roots of two binary trees `p` and `q`, check if they're the same — structurally identical with matching node values.

A strong demonstration of [[Binary Trees - Subtrees|the recursive nature of trees]].

## The recursive definition
`p` and `q` are the same tree if and only if **all** of the following hold:
1. `p.val == q.val`
2. `p.left` and `q.left` are the same tree
3. `p.right` and `q.right` are the same tree

Conditions 2 and 3 are answered by **calling the very function being implemented** — this is the core insight: since any subtree can be treated as its own tree, the exact same "is same tree" question applies recursively to the children.

Combined check: `p.val == q.val && isSameTree(p.left, q.left) && isSameTree(p.right, q.right)`

## Base cases
- Both `p` and `q` are `None` → `True` (two empty trees are trivially "the same" — both are empty)
- Exactly one of `p`/`q` is `None` (not both) → `False` (clearly not structurally identical)

**Sanity check with a single-node tree:** if `p` and `q` are both one-node trees with equal values, the value check passes, then both left/right recursive calls hit the "both `None`" base case and return `True` — correctly concluding the trees match.

## Recursive code
```python
class Solution:
    def isSameTree(self, p: TreeNode, q: TreeNode) -> bool:
        if p == None and q == None:
            return True

        if p == None or q == None:
            return False

        if p.val != q.val:
            return False

        left = self.isSameTree(p.left, q.left)
        right = self.isSameTree(p.right, q.right)
        return left and right
```

**The elegance of recursion here:** at the root, the subtrees could have thousands of nodes each — but you don't need to reason about that complexity directly. Trusting that the recursive call correctly answers the same question for smaller inputs is enough; the cascading calls handle the rest.

## Iterative code
```python
class Solution:
    def isSameTree(self, p: TreeNode, q: TreeNode) -> bool:
        stack = [(p, q)]
        while stack:
            p, q = stack.pop()
            if p == None and q == None:
                continue

            if p == None or q == None:
                return False

            if p.val != q.val:
                return False

            stack.append((p.left, q.left))
            stack.append((p.right, q.right))

        return True
```
Same structural checks as the recursive version, but instead of returning `True` early during traversal, it returns `False` as soon as any mismatch is found, and only returns `True` once the whole traversal completes without issue.

## Complexity
**O(n) time, O(n) space** worst case — identical reasoning to the other examples in this chapter (see [[Binary Trees - Iterative DFS]]).

#dsa #algorithms #trees #binary-trees #recursion

Related: [[Binary Trees - Subtrees]], [[Binary Trees - Lowest Common Ancestor Example]]
