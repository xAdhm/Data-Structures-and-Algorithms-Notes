# Graphs - State Variables in BFS

A recurring idea, first seen with [[Binary Trees - Path Sum Example|extra DFS arguments like `curr`]]: sometimes a plain "node" isn't enough information to correctly track progress through a problem — extra variables need to travel alongside the node.

## The generalization: "state," not just "node"
`seen` has always been described as preventing revisits to a **node** — but more precisely, it prevents revisiting the same **state**. In every earlier example, a node's identity fully described the state, so `state = node` and this distinction didn't matter. Once a problem needs extra variables (like "how many obstacle-removals do I have left," or "what color was the last edge crossed"), the *state* becomes `(node, extra_variable, ...)` — and `seen` must track combinations of these, not just the node alone.

## Impact on complexity
The general graph time complexity is more precisely **O(states + edges)**, not O(nodes + edges) — it just so happens that `states = nodes` when no extra variables are involved. When a state has multiple components, the total number of states is the **product** of each component's range. E.g. `m·n` possible node positions × `k` possible remaining-removals values = `m·n·k` total states.

## Two worked examples using this idea
- [[Graphs - Shortest Path with Obstacle Elimination Example]] — state = `(row, col, obstacles_remaining)`
- [[Graphs - Shortest Path with Alternating Colors Example]] — state = `(node, last_edge_color)`

#dsa #algorithms #graphs #queues

Related: [[Graphs - BFS Overview]], [[Binary Trees - Path Sum Example]]
