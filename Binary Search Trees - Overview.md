# Binary Search Trees - Overview

A **binary search tree (BST)** is a type of [[Binary Trees - Overview|binary tree]] with a special ordering property:

> For each node, all values in its left subtree are less than the node's value, and all values in its right subtree are greater than it.

This property implies all values in a BST must be **unique** (no duplicates — since "less than" and "greater than" are strict).

## Why BSTs are efficient
Operations like search, add, and remove run in **O(log n) average time** (`n` = number of nodes), using **binary search** (covered in a later chapter) — since at each node, you can eliminate an entire subtree from consideration.

## Searching a BST
Example: searching for `20` in a BST rooted at `23`.
- `23 > 20` → the entire right subtree can be ignored (everything there is `> 23 > 20`) → search left
- `20 > 8` → ignore the left subtree this time → search right
- `20 > 17` → ignore left again → search right
- Found `20`

Each comparison eliminates roughly half the remaining nodes — the same halving intuition as [[Time Complexity - Examples|logarithmic time complexity]].

**Worst case:** if the tree degenerates into a straight line (e.g. no right children at all — essentially a linked list shape), search becomes **O(n)**, since there's no branching left to eliminate.

## Key trivia: inorder traversal gives sorted order
Performing an [[Binary Trees - DFS Overview|inorder DFS]] (left → current → right) on a BST visits nodes in **sorted order**. This directly follows from the BST property and is a frequently-used trick — see [[Binary Search Trees - Minimum Absolute Difference Example]].

## Worked examples
- [[Binary Search Trees - Range Sum Example]] — pruning subtrees using the BST property
- [[Binary Search Trees - Minimum Absolute Difference Example]] — leveraging inorder traversal's sorted output
- [[Binary Search Trees - Validate BST Example]] — checking the BST property holds throughout

#dsa #algorithms #trees #binary-search-trees

Related: [[Binary Trees - Overview]], [[Binary Trees - DFS Overview]]
