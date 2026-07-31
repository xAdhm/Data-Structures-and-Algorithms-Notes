# Binary Trees - Subtrees

Arguably **the** most important concept for solving tree problems.

## Definition
A **subtree** of a tree is a chosen node together with **all of its descendants**. Trees are inherently **recursive** — any subtree can be treated as its own standalone tree, with the chosen node acting as *its* root.

## Illustrating with the company org-chart example
The whole company is a tree rooted at the CEO (see [[Binary Trees - Overview]]). Suppose the CTO has a direct report who is the SVP of Engineering, and every engineer reports up through this SVP. If you take the SVP and sever their connection to the CTO, what's left is **still a valid tree** — just now rooted at the SVP instead of the CEO. This new subtree represents the engineering department specifically, and it's structurally just as much "a tree" as the original whole-company tree was.

## Why this matters for solving problems
Because any node can be treated as the root of its own (sub)tree, tree problems can almost always be solved **recursively**: solve the problem for a node's left subtree, solve it for the right subtree, then combine those results with the current node's own data to get the answer for the whole tree rooted at the current node. This mirrors the [[Recursion - Breaking Down Problems (Fibonacci)|breaking-a-problem-into-subproblems]] approach from the recursion chapter — a subtree *is* a smaller instance of the exact same kind of problem (a tree), which is precisely what makes recursion so natural here.

**Terminology note:** the subtree rooted at a node reached via the root's `left` pointer is called the **left subtree** of the root; likewise for the right.

#dsa #algorithms #trees #binary-trees #recursion

Related: [[Binary Trees - Terminology]], [[Recursion - Breaking Down Problems (Fibonacci)]], [[Binary Trees - Code Representation]]
