# Graphs - Input Formats

Unlike [[Linked Lists - Overview|linked lists]] (given a `head`) or [[Binary Trees - Overview|binary trees]] (given a `root`), a graph **doesn't literally exist in memory** as an input — only "information about" a graph is given, and it's up to you to decide how to represent and traverse it in code.

Nodes are often labeled `0` to `n - 1`. Sometimes the problem won't explicitly say "this is a graph" — you may need to recognize it from a story (e.g. "there are n cities labeled 0 to n-1" → cities are nodes).

## Why pre-processing is usually needed
With trees, traversal was simple — at any node, just reference `node.left`/`node.right` directly. With graphs, a node can have **any number** of neighbors, and depending on the input format, finding them might require scanning the entire input every single time. Before traversing, it's usually worth **pre-processing** the input into a structure where "give me a node, get back its neighbors" is fast (typically O(1)) — usually a hash map.

**Facebook analogy:** if Facebook stored their whole social graph as a flat list of edges, finding "who are my friends" would mean scanning billions/trillions of connections worldwide. Pre-building a lookup structure (e.g. per-user friend lists) is what makes fetching your own friends list instant.

## Format 1: array of edges
2D array where each `[x, y]` means an edge exists between `x` and `y`. Could be directed or undirected — stated in the problem.

**Why you can't traverse this directly:** finding node `0`'s neighbors means scanning the *entire* edge list; moving to a neighbor means scanning the entire list again — repeated at every node. Very slow.

**Fix — pre-process into a hash map:** map each node to a list of its neighbors. For each `[x, y]`, append `y` to `graph[x]`'s list; if undirected, also append `x` to `graph[y]`'s list. After this, `graph[0]` instantly gives node 0's neighbors.

```python
from collections import defaultdict

def build_graph(edges):
    graph = defaultdict(list)
    for x, y in edges:
        graph[x].append(y)
        # graph[y].append(x)
        # uncomment the above line if the graph is undirected

    return graph
```

Example: `edges = [[0, 1], [1, 2], [2, 0], [2, 3]]` represents a graph that only exists conceptually — never as an actual in-memory node/pointer structure the way a tree does.

## Format 2: adjacency list
Nodes numbered `0` to `n-1`; input is a 2D array `graph` where `graph[i]` is the list of `i`'s outgoing neighbors directly.

Example: `graph = [[1], [2], [0, 3], []]` represents the same graph as above.

**No pre-processing needed** — this format is already exactly what you'd build by hand-processing an edge list. Most convenient format to work with directly.

## Format 3: adjacency matrix
Nodes numbered `0` to `n-1`; input is an `n x n` matrix `graph`, where `graph[i][j] == 1` means an edge exists from `i` to `j`.

**Two options:**
1. Use it directly — at each node, scan its row (`graph[node]`) to find neighbors (`graph[node][i] == 1`)
2. Pre-process into a hash map (same idea as the edge-list format) — iterate the whole matrix once, and for every `graph[i][j] == 1`, append `j` to `i`'s neighbor list

Both approaches have **O(n²)** time complexity overall — pre-processing helps more when nodes have few neighbors relative to `n`, since it avoids re-scanning a mostly-empty row at every single node during traversal.

## Format 4: implicit matrix/grid graph
A more subtle but very common format: input is a 2D matrix, and the *problem's story* defines the graph — e.g. "each square of the matrix is a village; villages trade with the villages directly above, below, left, or right of them."

Here, **each cell `(row, col)` is a node**, and neighbors are determined by the story, not stated explicitly as edges — in this example: `(row-1, col)`, `(row, col-1)`, `(row+1, col)`, `(row, col+1)` (whichever are in bounds).

**Key distinction from the other formats:** nodes aren't labeled `0` to `n-1` here — each matrix element *is* a node, and you have to carefully read the problem to figure out what counts as an edge.

#dsa #algorithms #graphs #hash-map

Related: [[Graphs - Overview]], [[Graphs - Terminology]], [[Hashing - Hash Maps]]
