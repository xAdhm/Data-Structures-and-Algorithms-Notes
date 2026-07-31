# Binary Trees - BFS vs DFS

## When it doesn't matter
For many binary tree problems, [[Binary Trees - DFS Overview|DFS]] traversal order (preorder/inorder/postorder) doesn't matter — only that every node gets visited. In those same problems, [[Binary Trees - BFS Overview|BFS]] would also work fine, since every node's visit carries enough self-contained information regardless of visit order.

Given this, DFS is usually preferred by default when either would work: it requires less code and is easier to implement (especially recursively). Most people default to DFS unless BFS offers a specific advantage.

## When BFS genuinely shines
BFS makes more algorithmic sense specifically for problems that need to handle nodes **according to their level** — e.g. [[Binary Trees - Right Side View Example]] and [[Binary Trees - Largest Value in Each Row Example]]. DFS *can* solve these too (with extra bookkeeping to track depth), but BFS's natural level-by-level structure fits these problems more directly.

## Interview trivia: drawbacks of each
**DFS's main disadvantage:** can waste huge amounts of time searching for a value that happens to be shallow but in the "wrong" priority direction. E.g. searching a huge tree prioritizing left-before-right, when the target is the root's right child — DFS would traverse the *entire* left subtree (potentially millions of nodes) before ever reaching a node that's really just one step from the root.

**BFS's main disadvantage:** wastes time if the target is deep — it must exhaustively process every shallower level first before reaching the bottom.

## Space complexity comparison
- **DFS:** space linear in the tree's **height** (max depth) — since that's the call stack's worst-case depth.
- **BFS:** space linear in the **widest level** (the level with the most nodes) — since that's the max queue size at any point.

**Perfect binary tree example:** DFS uses **O(log n)** space (height of a perfect tree), while BFS uses **O(n)** space (the final level alone can hold `n/2` nodes).

**Lopsided tree example (e.g. a straight line):** BFS uses **O(1)** space (each level only ever has 1 node), while DFS uses **O(n)** space (call stack depth = number of nodes). This is an edge case though — a more "full," balanced tree is the typical expectation.

**Takeaway:** neither is universally more space-efficient — it depends entirely on the tree's shape.

#dsa #algorithms #trees #binary-trees

Related: [[Binary Trees - DFS Overview]], [[Binary Trees - BFS Overview]], [[Binary Trees - Iterative DFS]]
