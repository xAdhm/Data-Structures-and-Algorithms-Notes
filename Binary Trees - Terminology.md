# Binary Trees - Terminology

Core vocabulary needed for the rest of the [[Binary Trees - Overview|binary trees]] chapter.

## Root
The node at the "top" of the tree. Every node in the tree is reachable starting from the root. In most tree problems, the root is given as the input — directly analogous to how `head` was given as input for [[Linked Lists - Overview|linked list]] problems.

## Parent / child
If node `A` has an edge to node `B` (`A -> B`), `A` is the **parent** of `B`, and `B` is a **child** of `A`.

## Leaf
A node with **no children** is a **leaf node**. The leaves are the "endpoints" of the tree.

## Depth
The **depth** of a node is how far it is from the root.
- Root's depth = **0**
- Every child's depth = **parent's depth + 1**

So the root's direct children have depth 1, their children have depth 2, and so on.

## Subtree — the most important concept
Covered in detail in [[Binary Trees - Subtrees]] — a **subtree** is a node and all of its descendants, and can itself be treated as a standalone tree. This recursive property is the foundation for how nearly all tree problems get solved.

#dsa #algorithms #trees #binary-trees

Related: [[Binary Trees - Overview]], [[Binary Trees - Subtrees]]
