# Tries - Search Suggestions System Example

## Problem: 1268. Search Suggestions System
Given `products` and `searchWord`, after each character of `searchWord` is typed, suggest up to 3 products sharing that prefix — the 3 lexicographically smallest if more than 3 match. Return the suggestions after each character typed.

## Why brute force is too slow
For each prefix (one per character typed), scanning all of `products` and checking matches costs **O(n·m²)**, where `n = len(products)`, `m = len(searchWord)` (the `m²` comes from checking `m` prefixes, each costing up to `m` to compare).

## The trie-based improvement
Build a [[Tries - Overview|trie]] from `products` once — **O(n·k)**, `k` = average product name length. Once built, **each node itself directly represents a prefix** (root = empty string, per [[Tries - Overview]]) — so looking up all matches for any prefix becomes a single **O(m)** walk down the trie, no re-scanning needed.

**Storing the answer directly on each node:** give every `TrieNode` a `suggestions` attribute holding (up to) the 3 lexicographically smallest products sharing that node's prefix. Keep it sorted and capped at size 3 as the trie is built — cheap since the list never exceeds 3 elements.

## Building the trie with suggestions maintained inline
For each product, walk/create nodes character by character; at **every** node visited (i.e. every prefix of the product), append the product to that node's `suggestions`, re-sort, and trim to size 3 if needed.

## Code
```python
class TrieNode:
    def __init__(self):
        self.children = {}
        self.suggestions = []

class Solution:
    def suggestedProducts(self, products: List[str], searchWord: str) -> List[List[str]]:
        root = TrieNode()
        for product in products:
            node = root
            for c in product:
                if c not in node.children:
                    node.children[c] = TrieNode()
                node = node.children[c]
                node.suggestions.append(product)
                node.suggestions.sort()
                if len(node.suggestions) > 3:
                    node.suggestions.pop()

        ans = []
        node = root
        for c in searchWord:
            if c in node.children:
                node = node.children[c]
                ans.append(node.suggestions)
            else:
                # deadend reached
                node.children = {}
                ans.append([])
        return ans
```

**Traversal:** walk `searchWord` character by character starting at the root; at each step, if the next character exists as a child, move there and read `suggestions` directly (already precomputed and correctly sorted/trimmed). If a character has no matching child, every remaining prefix is a guaranteed dead end — append empty lists for the rest without further lookup work.

## Complexity
Building: **O(n·k)**. Traversal: **O(m)**. **Total: O(n·k + m) time** — a substantial improvement over the O(n·m²) brute force, since `k` (average product length) is typically small.

#dsa #algorithms #tries

Related: [[Tries - Overview]]
