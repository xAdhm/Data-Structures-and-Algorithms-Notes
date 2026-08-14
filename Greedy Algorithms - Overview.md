# Greedy Algorithms - Overview

A **greedy algorithm** makes the **locally optimal** decision at every step.

## Breaking down the definition
- **"Optimal"** depends on the problem — e.g. if maximizing a sum, the optimal choice between two numbers is picking the larger one.
- **"Local"** means the decision only considers options available *right now* — based on current information, without weighing any future consequences.

Most greedy problems ask for a max or min of something, though not exclusively.

## The pizza delivery example
Delivering to 5 houses, always choosing the *nearest remaining* house at each step, could produce a worse total route than some other order — e.g. if there's a "bridge" (shortcut) between two houses that a different ordering would have exploited. At each step, only the immediate next choice was considered — no lookahead into how that choice affects future steps. This illustrates the core risk of greedy approaches: **locally optimal choices don't always add up to a globally optimal result.**

## Connection to heaps
Many [[Heaps - Overview|heap]]-based algorithms are inherently greedy — a heap gives you the max/min element, and greedy approaches typically choose the max/min at each step. Most examples from the [[Heaps - Overview|previous heaps chapter]] can be classified as greedy algorithms (e.g. always combining the two smallest sticks in [[Heaps - Overview|Minimum Cost to Connect Sticks]], always halving the current largest pile).

## Connection to sorting
Many greedy problems **sort the input upfront** — since sorting makes it convenient to repeatedly access the max/min element in order, which is exactly what a greedy strategy usually needs.

## The hard part: proving it works
**Implementing** a greedy algorithm is typically easy. **Proving the greedy strategy is actually correct** is the hard part. A greedy approach can often produce an answer that's *close* to correct but still wrong — and for LeetCode/interview purposes, "close" isn't good enough; a fully correct algorithm is required.

## Real-world context: approximations are sometimes good enough
Outside of interviews, greedy algorithms can be valuable even when not perfectly correct, because they trade a small accuracy loss for a big efficiency gain. Example: the **travelling salesman problem (TSP)** — a greedy approach gives an answer typically only ~25% off from optimal, in **O(n²)** time. The best known *exact* solution is O(2ⁿ), and many believe no dramatically faster exact algorithm exists at all.

## "Greedy" is an approach, not a tool
Unlike a data structure or a single named algorithm, "greedy" is a general **way of approaching** a problem — there isn't a fixed technique to memorize. The real skill is **recognizing when a greedy strategy applies** to a given problem. Greedy algorithms, when they do apply, are usually very efficient — making that recognition skill valuable.

#dsa #algorithms #greedy

Related: [[Heaps - Overview]], [[Heaps - Top K Pattern]]
