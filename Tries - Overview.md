# Tries - Overview

A **trie** (aka **prefix tree**) is a tree data structure that stores **characters of a string at each node**. Every path from the root to any node represents a string — specifically, the sequence of characters along that path.

Referenced earlier as a template in [[Code Templates - Quick Reference]] — this note covers the concept in full.

## Use case: efficient string searching/matching
Given a huge word list and a stream of characters (e.g. someone typing), a trie lets you track which words share the characters typed so far as a **prefix** — far more efficiently than repeatedly scanning the whole word list.

## Building a trie
```python
# note: using a class is only necessary if you want to store data at each node.
# otherwise, you can implement a trie using only hash maps.
class TrieNode:
    def __init__(self):
        # you can store data at nodes if you wish
        self.data = None
        self.children = {}

def build_trie(words):
    root = TrieNode()
    for word in words:
        curr = root
        for c in word:
            if c not in curr.children:
                curr.children[c] = TrieNode()
            curr = curr.children[c]
        # at this point, you have a full word at curr
        # you can perform more logic here to give curr an attribute if you want

    return root
```

Each node's `children` is a hash map from character → child `TrieNode`. Walking a word inserts one node per new character encountered, reusing existing nodes for shared prefixes.

**Building cost: O(n · k)**, where `n = len(words)`, `k` = average word length.

See [[Tries - Search Suggestions System Example]] for a full worked application.

#dsa #algorithms #tries #hashing

Related: [[Code Templates - Quick Reference]], [[Hashing - Hash Maps]], [[Tries - Search Suggestions System Example]]
