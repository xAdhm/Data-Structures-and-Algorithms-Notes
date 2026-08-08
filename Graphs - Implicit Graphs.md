# Graphs - Implicit Graphs

Every graph example so far has conformed to one of the standard [[Graphs - Input Formats|input formats]] (adjacency list, adjacency matrix, edge array, or explicit grid/matrix) — which made it relatively easy to spot "this is a graph problem." Some problems say so explicitly; others hint at it with a story (e.g. "cities connected by roads").

Sometimes a graph is far more subtle — the input doesn't resemble any standard graph format at all.

## The generalizing insight
A graph is fundamentally just **any abstract collection of elements connected by some abstract relationship**. Whenever a problem involves **transitioning between states**, ask: can the states be treated as nodes, and the transition rules as edges?

**Another strong signal:** if the problem asks for the shortest path, fewest operations, or minimum number of moves/steps — that's a great candidate for [[Graphs - BFS Overview|BFS]], even if nothing about the problem looks graph-like on the surface.

## Worked examples
- [[Graphs - Open the Lock Example]] — lock combinations as nodes, single-digit turns as edges
- [[Graphs - Evaluate Division Example]] — variables as nodes, division equations as **weighted** edges

#dsa #algorithms #graphs

Related: [[Graphs - Input Formats]], [[Graphs - BFS Overview]]
