# Dynamic Programming - When to Use It

Two main characteristics suggest a [[Dynamic Programming - Overview|DP]] approach:

## 1. Asking for an optimal value or a count
- "What is the minimum cost of doing ..."
- "What is the maximum profit of ..."
- "How many ways are there to ..."
- "What is the longest possible ..."

**Caveat:** not every problem phrased this way needs DP, and not every DP problem is phrased this way — this is a useful heuristic, not a guarantee.

## 2. Decisions affect future decisions
At each step, a "decision" must be made (e.g. picking between two elements), and that decision **constrains or affects** what decisions are available later (e.g. "if you take element x, you can't take element y later").

## This is what separates DP from greedy
[[Greedy Algorithms - Overview|Greedy]] assumes local decisions **don't** meaningfully affect future decisions — the locally optimal choice is always safe. DP problems are exactly the ones where that assumption **breaks down**.

### Illustrating example: House Robber
Rob houses along a street (`nums[i]` = money in house `i`); robbing two **adjacent** houses triggers an alarm. Maximize total money robbed.

With `nums = [2,7,9,3,1]`, a greedy approach comparing `2` vs `7` would take `7` (locally better) — but taking `7` **rules out** taking `9` next (adjacent). The actual optimal answer is `2 + 9 + 1 = 12`, achieved specifically by **not** greedily taking the `7`. This is the textbook illustration of "being greedy in a decision affected a future decision and led to the wrong answer" — precisely the second DP characteristic.

#dsa #algorithms #dynamic-programming #greedy

Related: [[Dynamic Programming - Overview]], [[Greedy Algorithms - Overview]]
