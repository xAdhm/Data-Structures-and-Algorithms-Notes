# Binary Trees - Iterative DFS

All three DFS types ([[Binary Trees - DFS Overview]]) can be implemented iteratively, but postorder and inorder are noticeably more complex to implement iteratively than preorder. Since traversal type rarely matters, a **preorder iterative implementation** is the common go-to when recursion isn't wanted or allowed.

## Why a stack
Since DFS needs to backtrack after fully exploring a branch, an iterative implementation needs an explicit [[Stacks - Overview|stack]] to replicate what the call stack does automatically in recursion.

## The trick: pair each node with extra state
Recursive versions get "extra" per-call data for free (e.g. current depth) because each function call has its own local variables. Iteratively, that data has to be stored explicitly alongside each node on the stack — e.g. as a tuple `(node, depth)` in Python. Other languages without tuple literals need a pair object or parallel stacks.

## General iterative template
- Push the root (with any needed associated state) onto the stack.
- While the stack isn't empty: pop a node (this is equivalent to one function call in the recursive version), do the problem's logic, then push its children (with updated state) if they exist.

## Important gotcha: visit order is reversed from insertion order
If you push `node.left` before `node.right`, popping (LIFO) visits `node.right` **first** — the opposite of the recursive version, which visits left first by default. This is irrelevant when the problem only cares that *all* nodes get visited (order-independent), but it's worth understanding explicitly: **iterative traversal order is the reverse of insertion order**, because of how a stack pops.

## Complexity (applies broadly to DFS tree problems, iterative or recursive)
- **Time: usually O(n)**, where `n` = total nodes — each node visited exactly once, O(1) work per node. If a problem does O(k) work per node instead of O(1), time becomes **O(n·k)**.
- **Space:**
  - Recursive: call stack usage counts as space. Worst case **O(n)** if the tree degenerates into a straight line (essentially a linked list shape).
  - Iterative: the explicit stack's max size follows the same worst-case bound, **O(n)**.
  - Best case for either (a **complete** tree — every node has 0 or 2 children, all levels full except possibly the last): **O(log n)**. But O(n) is the safe general answer to give, since it covers the worst case.

#dsa #algorithms #trees #binary-trees #stacks

Related: [[Binary Trees - DFS Overview]], [[Stacks - Overview]]
