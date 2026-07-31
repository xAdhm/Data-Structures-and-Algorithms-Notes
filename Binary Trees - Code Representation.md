# Binary Trees - Code Representation

Just like [[Linked Lists - Overview|linked lists]], binary trees are implemented with objects of a custom class.

## Standard class definition
```python
class TreeNode:
    def __init__(self, val, left, right):
        self.val = val
        self.left = left
        self.right = right
```

## Working with it
- Binary tree problems typically give you a reference to the **root** as input.
- Access the root's left subtree via `root.left`, and the right subtree via `root.right`.
- Each node carries a `val`, same as a linked list node.

## Null children
In a linked list, the tail's `next` pointer is `null`/`None`. In a binary tree:
- If a node has no left child, `node.left` is `None`
- If a node has no right child, `node.right` is `None`
- If **both** are `None`, the node is a [[Binary Trees - Terminology|leaf]]

#dsa #algorithms #trees #binary-trees

Related: [[Binary Trees - Overview]], [[Binary Trees - Subtrees]], [[Linked Lists - Overview]]
