# Graphs - Terminology

Core vocabulary for the [[Graphs - Overview|graphs]] chapter.

## Directed vs. undirected edges
- **Directed:** traversable in only one direction. An edge `A -> B` lets you move `A` to `B`, but not back. Drawn as arrows.
- **Undirected:** traversable both ways — `A -> B` and `B -> A` both valid. Drawn as plain lines.

**Binary trees are directed graphs** — you can reach a child from its parent, but not the reverse (no way to access `node.parent`).

## Connected components
A **connected component** is a group of nodes all reachable from one another via edges. A graph can have one or many separate connected components (islands of nodes with no edges between the islands).

**Binary trees always have exactly one connected component** — every node is reachable starting from the root.

## Indegree / outdegree / neighbors
A node can have any number of edges. For a **directed** graph:
- **Indegree** — number of edges entering the node (ways to *reach* it)
- **Outdegree** — number of edges leaving the node (ways to *leave* it)

Nodes connected by an edge are **neighbors**. E.g. in `A <-> B <-> C`: `A` and `B` are neighbors, `B` and `C` are neighbors, but `A` and `C` are not.

**Binary tree equivalents:** every node except the root has indegree 1 (from its parent); every node has outdegree 0, 1, or 2 (outdegree 0 = a [[Binary Trees - Terminology|leaf]]). Trees use "parent"/"child" instead of "neighbor" specifically because edges are directed and hierarchical.

## Cyclic vs. acyclic
- **Cyclic:** the graph contains a cycle — a path that leads back to a previously visited node, same [[Fast and Slow Pointers - Cycle Detection|cycle concept]] introduced for linked lists.
- **Acyclic:** no cycles exist.

**Binary trees are always acyclic by definition** — the strict parent/child structure makes cycles structurally impossible.

#dsa #algorithms #graphs

Related: [[Graphs - Overview]], [[Fast and Slow Pointers - Cycle Detection]], [[Binary Trees - Terminology]]
