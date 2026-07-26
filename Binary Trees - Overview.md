# Binary Trees - Overview

A **tree** is a type of [[Trees and Graphs - Nodes, Vertices, and Edges|graph]] — like linked lists, there are multiple types of trees, but this course focuses on **binary trees**.

## Root, parent, child
- The start of a linked list was the **head**; the start of a tree is the **root**.
- In a linked list, a node's pointer led to the *next* node. In a tree, a node has pointers to its **children**. If node `A` points to node `B`, then `B` is a **child** of `A`, and `A` is the **parent** of `B`.
- The root is the only node with **no parent**.
- A node can have **at most one parent** (this is a defining structural rule of trees).

## What makes it "binary"
In a binary tree, every node has **at most 2 children**, referred to as the **left child** and **right child**. Left vs. right is purely a naming/graphical convention — there's no inherent structural difference between them.

**Summary:** a binary tree is a collection of nodes where every node has 0–2 children, and every node except the root has exactly 1 parent.

## Real-world tree examples
Trees (not necessarily binary) show up constantly:
- **File systems** — root directory as root, subfolders/files as children
- **Comment threads** (Reddit, Twitter/X, etc.) — original post as root, comments/replies as children
- **Company org charts** — CEO as root, direct reports as children

**Company example, in detail:** if `A` manages `B`, draw an edge `A → B`. The CEO is the root (not managed by anyone). If the CEO has 6 direct reports (C-suite), the CEO has 6 children — **not** a binary tree, since binary trees cap children at 2. Each C-suite member has their own reports (VPs), who have their own reports (directors), and so on.

**What makes an org chart a tree, structurally:** each person has exactly one manager (parent), and the whole structure is **connected** — starting from any employee and repeatedly tracing "who's their manager" always eventually reaches the CEO.

#dsa #algorithms #trees #binary-trees

Related: [[Trees and Graphs - Nodes, Vertices, and Edges]], [[Binary Trees - Terminology]], [[Binary Trees - Code Representation]]
