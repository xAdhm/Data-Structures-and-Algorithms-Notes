# Binary Trees - DFS Overview

Prerequisite: solid understanding of [[Binary Trees - Overview|what a binary tree is]] and [[Recursion - Overview|recursion]].

**Tree traversal** = how we access a tree's elements — mandatory for solving any tree problem.

## From linked lists to trees
Recall [[Linked Lists - Pointer Mechanics|linked list traversal]]:
```python
def get_sum(head):
    ans = 0
    while head:
        ans += head.val
        head = head.next

    return ans
```
Binary tree traversal follows the same idea — start at the root, move via child pointers (`.left`/`.right`) instead of `.next`. The key difference: linked lists are usually traversed **iteratively**; binary trees are usually traversed **recursively**, since [[Binary Trees - Subtrees|each subtree is itself a tree]] — a natural fit for recursive thinking.

## Two main traversal types
1. **Depth-first search (DFS)** — covered in this note. Three flavors: preorder, inorder, postorder (the choice rarely matters in practice).
2. **Breadth-first search (BFS)** — covered in a later article.

## DFS: prioritize depth
DFS goes as far down the tree as possible in one direction (until hitting a leaf) before backtracking to explore the other direction. E.g. if "left" is the priority: follow `node.left` exclusively until the entire left subtree is exhausted, *then* explore right.

Visualize it like branches on a real tree: DFS commits to one branch, follows it to the end, then backtracks to find the next unexplored branch. Because of this backtracking need, DFS is naturally implemented with **recursion** (though it can also be done iteratively using an explicit [[Stacks - Overview|stack]] — see [[Binary Trees - Iterative DFS]]).

## Simplest DFS — visit every node
```python
def dfs(node):
    if node == None:
        return
    dfs(node.left)
    dfs(node.right)
    return
```

Each call to `dfs(node)` "visits" that node. Many calls to `dfs` exist **simultaneously** on the call stack, each with its own version of `node` — same concept as [[Recursion - Call Stack and Execution Order|the call stack behavior]] covered in the recursion chapter.

## General DFS structure (applies across nearly all tree problems)
1. Handle base case(s) — usually an empty tree (`node == None`)
2. Do some logic for the current node
3. Recursively call on the current node's children
4. Return the answer

**Steps 2 and 3's order is what distinguishes the three DFS types.** The core mental model: each function call solves and returns the answer *as if the subtree rooted at the current node were the entire input*.

## The three DFS orderings
Using a talking-point tree with root `0`, illustrating each:

### Preorder — logic happens *before* recursing into children
```python
def preorder_dfs(node):
    if not node:
        return
    print(node.val)
    preorder_dfs(node.left)
    preorder_dfs(node.right)
    return
```
Visits nodes in the same order the function calls themselves happen. Example output order: `0, 1, 3, 4, 6, 2, 5`.

### Inorder — logic happens *between* left and right children
```python
def inorder_dfs(node):
    if not node:
        return
    inorder_dfs(node.left)
    print(node.val)
    inorder_dfs(node.right)
    return
```
No logic runs until reaching a node with no left child (since the left call takes priority). Example output order: `3, 1, 4, 6, 0, 2, 5`. For any node: its value prints only after its entire left subtree, and before its entire right subtree.

### Postorder — logic happens *after* both children
```python
def postorder_dfs(node):
    if not node:
        return
    postorder_dfs(node.left)
    postorder_dfs(node.right)
    print(node.val)
    return
```
No logic until reaching a leaf; the root is always the *last* node processed. Example output order: `3, 6, 4, 1, 5, 2, 0`. For any node: nothing in its right subtree prints until its entire left subtree has printed, and its own value prints last of all three.

**Naming logic:** Pre = before children, In = in the middle of children, Post = after children.

## Practical note
Since recursion makes switching between the three trivial (just reorder a couple of lines), and for many problems the traversal *type* genuinely doesn't matter — only that all nodes get visited — the distinction is mostly good interview trivia rather than a decision that changes your solution's correctness.

#dsa #algorithms #trees #binary-trees #recursion

Related: [[Binary Trees - Subtrees]], [[Recursion - Call Stack and Execution Order]], [[Binary Trees - Iterative DFS]]
