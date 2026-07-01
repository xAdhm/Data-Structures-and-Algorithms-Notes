# 📚 Data Structures & Algorithms Notes
A personal Obsidian vault of DSA study notes — complexity analysis and four core problem-solving patterns (two pointers, sliding window, prefix sum, recursion), written as linked, taggable Markdown notes rather than a single wall of text.
---
## 🗂️ What's Inside
This is a **notes vault, not a codebase** — there's no code, no dependencies, and nothing to install or run. Each `.md` file is one focused concept, cross-linked to related notes via `[[wikilinks]]` and tagged with `#hashtags` for topic filtering. It's built for [Obsidian](https://obsidian.md) (the `.obsidian/` config folder is included) but every file is plain Markdown and readable anywhere, including directly on GitHub.
---
## 🧭 How These Notes Are Organized
Files follow a `Topic - Subtopic.md` naming convention. Most topics have an `Overview` note that introduces the concept and links out to the more specific notes underneath it:

- **Foundations** — `What Is an Algorithm`, `Big O - Overview`, `Big O - Rules for Calculating Complexity`, `Time Complexity - Examples`, `Space Complexity - Examples`
- **Arrays & Strings** — `Arrays and Strings - Overview`, `Arrays and Strings - Time Complexity of Operations`
- **Two Pointers** — `Two Pointers - Overview`, `Two Pointers - Converging Pointers Method`, `Two Pointers - Two Iterables Method`
- **Sliding Window** — `Sliding Window - Overview`, `Sliding Window - Fixed Window Size`, `Sliding Window - Dynamic Window Size`, `Sliding Window - Counting Valid Subarrays`, `Sliding Window - Why It's Efficient`
- **Prefix Sum** — `Prefix Sum - Overview`, `Prefix Sum - Range Sum Queries Example`, `Prefix Sum - Space Optimization`
- **Recursion** — `Recursion - Overview`, `Recursion - Base Cases`, `Recursion - Breaking Down Problems (Fibonacci)`, `Recursion - Call Stack and Execution Order`
---
## 🚀 How to Use This Vault
### 1. Clone the repo
```bash
git clone git@github.com:xAdhm/Data-Structures-and-Algorithms-Notes.git
```
### 2. Open it as a vault in Obsidian
Open Obsidian → **Open folder as vault** → select the cloned folder. The included `.obsidian/` settings will load your core plugins, appearance, and the pre-built graph view.
### 3. Navigate however suits you
- Start from any `Overview` note and follow `[[wikilinks]]` to related notes.
- Use Obsidian's **Graph View** to see how topics connect visually.
- Search or filter by tag (`#dsa`, `#two-pointers`, `#sliding-window`, etc. — full list below) to jump straight to a topic.
- No Obsidian? Every file is plain Markdown — browse them directly in this GitHub repo; the `[[wikilink]]` syntax just won't be clickable outside Obsidian.
---
## 📖 Topic Breakdown
### Big O & Complexity
Covers what Big O measures (time vs. space), the convention of using `n` (or multiple variables for multiple inputs) for input size, the standard complexity classes from `O(1)` to `O(2ⁿ)`, why worst case is the default when describing an algorithm, plus separate worked-example notes for time and space complexity and a note on the specific rules for calculating Big O (e.g. dropping constants, amortized analysis).
---
### Arrays & Strings
Baseline note on treating arrays/strings as the default input type for most problems in this vault, plus a breakdown of the time complexity of common operations (access, search, insert, delete) on each.
---
### Two Pointers
Introduces the pattern as "two index variables moving along one or more iterables" rather than a single fixed algorithm, then splits into its two common shapes: pointers converging from opposite ends of one iterable, and pointers advancing in lockstep across two separate iterables. Notes why the technique typically achieves O(n) time / O(1) space over a brute-force O(n²) approach.
---
### Sliding Window
Covers the fixed-size and dynamic-size variants of the pattern, a worked example on counting valid subarrays, and a dedicated note on *why* sliding window is efficient (avoiding redundant re-scanning of overlapping subarrays that a naive nested-loop approach would repeat).
---
### Prefix Sum
Covers the core idea (precomputing cumulative sums to answer range-sum queries in O(1) after O(n) preprocessing), a worked range-sum-query example, and a note on reducing the technique's space usage.
---
### Recursion
Covers what defines a recursive solution, the necessity and structure of base cases, how the call stack drives execution order, and a worked breakdown of Fibonacci as the canonical example of splitting a problem into smaller subproblems.
---
## 🏷️ Tag Conventions
Every note ends with one or more hashtags for filtering in Obsidian's search. Current tags in use, with usage counts:

| Tag | Count | Meaning |
|---|---|---|
| `#dsa` | 22 | Applied to virtually every note — the vault-wide tag |
| `#algorithms` | 22 | Same as above, paired with `#dsa` on nearly every note |
| `#arrays` | 12 | Notes involving array-based problems/techniques |
| `#strings` | 7 | Notes involving string-based problems/techniques |
| `#big-o` | 6 | Complexity-analysis notes |
| `#sliding-window` | 5 | Sliding window pattern notes |
| `#recursion` | 4 | Recursion notes |
| `#two-pointers` | 3 | Two pointers pattern notes |
| `#prefix-sum` | 3 | Prefix sum pattern notes |
| `#time-complexity`, `#space-complexity`, `#fibonacci`, `#amortized-analysis` | 1 each | Single-note, more specific tags |
---
## 📝 Notes for Other Learners
- **Every note ends with a `Related:` line** linking to adjacent notes via `[[wikilinks]]` — if you're adding a new note, follow that convention so it stays connected to the graph instead of becoming an orphan page.
- **`Overview` notes are entry points, not summaries of everything below them** — they introduce the concept and link out, but the real detail (worked examples, specific method variants) lives in the subtopic notes. Start at the Overview when learning a topic for the first time.
- **Tags are intentionally broad + specific together** (e.g. a two-pointers note carries `#dsa #algorithms #two-pointers #arrays`) — when adding tags to a new note, keep both the vault-wide tags (`#dsa`, `#algorithms`) and at least one topic-specific tag so it's findable both ways.
- **This vault currently stops at four patterns** (two pointers, sliding window, prefix sum, recursion) plus foundational complexity notes — there's no coverage yet of trees, graphs, dynamic programming, heaps, or sorting/searching algorithms, if you're extending it.
