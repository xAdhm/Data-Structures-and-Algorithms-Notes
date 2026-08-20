# Backtracking - Overview

The most brute-force way to solve a problem: **exhaustive search** — generate every possibility, then check each one for validity.

## Motivating example: generating strings of length n
With letters a-z, generating all strings of length `n` gives **26ⁿ** possibilities (each of the `n` positions independently has 26 choices). Visualize this as a **tree**: the root is the empty string, every node has 26 children, and following a path from root to a leaf spells out a string. The tree's depth is `n`; leaf nodes are complete candidate strings.

## Adding a constraint
Say we only want strings meeting some constraint. **Exhaustive search still generates all 26ⁿ candidates**, then filters — giving **O(k · 26ⁿ)** time, where `k` = cost to check the constraint. Ridiculously slow.

## Backtracking: prune paths early
**Backtracking** efficiently runs through possibilities by **abandoning ("pruning") a path** as soon as it's determined the path can't lead to a valid solution — same intuition as [[Binary Search Trees - Overview|BST search]] discarding an entire subtree once you know the target can't be there. Since subtree sizes grow **exponentially** with depth, pruning early saves enormous amounts of wasted computation.

**Example:** if the constraint is "only vowels allowed," backtracking discards every subtree containing a non-vowel choice immediately — improving from **O(26ⁿ)** down to **O(5ⁿ)** (5 vowels instead of 26 letters), rather than generating all 26ⁿ strings and filtering afterward.

## Exhaustive search vs. backtracking, summarized
- **Exhaustive search:** generate all possibilities, then check each for validity.
- **Backtracking:** prune invalid paths *during* generation, producing far fewer candidates overall.

## When to reach for backtracking
Great fit whenever a problem asks you to **find all of something**, or there's no clear shortcut besides checking all logical possibilities. **Strong LeetCode signal:** very small input constraints (`n ≤ ~15` or so) — backtracking algorithms are typically exponential time, so tiny bounds are often a deliberate hint. In real interviews, constraints usually aren't stated explicitly, so recognizing the *shape* of a backtracking problem (rather than relying on given bounds) is the more reliable skill to build.

## Implementation: recursion
Backtracking is almost always implemented **recursively** — doesn't meaningfully make sense iteratively. Typically involves building something incrementally, either directly (e.g. an array) or indirectly (state tracked via variables).

## General template
```
// let curr represent the thing you are building
// it could be an array or a combination of variables

function backtrack(curr) {
    if (base case) {
        Increment or add to answer
        return
    }

    for (iterate over input) {
        Modify curr
        backtrack(curr)
        Undo whatever modification was done to curr
    }
}
```

## Mapping the template back to the tree analogy
- Each call to `backtrack` = a node in the tree.
- Each iteration of the `for` loop = a child of the current node.
- Calling `backtrack` inside the loop = moving down to that child.
- **The "undo" step is the actual "backtracking"** — moving back up from a child to its parent, restoring `curr` to how it was before that branch was explored.
- The path from root to the current node = the candidate currently being built.
- Leaf nodes = complete candidates (base case reached).
- The root = an empty candidate, representing where the very first `backtrack` call starts from.

This chapter uses tree diagrams throughout to visualize backtracking — a very intuitive lens for these problems, similar to how [[Binary Trees - DFS Overview|DFS on binary trees]] was visualized as branch-by-branch exploration.

#dsa #algorithms #backtracking #recursion

Related: [[Recursion - Overview]], [[Binary Trees - DFS Overview]], [[Binary Search Trees - Overview]]
