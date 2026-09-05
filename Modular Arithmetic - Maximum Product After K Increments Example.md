# Modular Arithmetic - Maximum Product After K Increments Example

## Problem: 2233. Maximum Product After K Increments
Given non-negative integers `nums` and integer `k`: each operation increments any one element by 1. Return the maximum product achievable after at most `k` operations, **modulo 10^9 + 7**.

## Establishing the greedy strategy
Always increment the **currently smallest** element. Mathematical justification: given `x > y`, incrementing `x` gives `(x+1)*y = xy + y`, while incrementing `y` gives `x*(y+1) = xy + x`. Since `x > y`, the second product is larger — so incrementing the smaller number always yields a bigger gain. (Same [[Greedy Algorithms - Overview|greedy]] shape as earlier chapter examples.)

## Finding the smallest element repeatedly
This is the [[Heaps - Overview|"repeatedly find the minimum"]] pattern — use a min heap. Pop the smallest, increment it by 1, push it back. Repeat `k` times.

## Why the modulus matters here
After all increments, multiplying every element together can produce a genuinely enormous number — computing the **full** product first and only taking `% MOD` at the very end risks overflow (in languages with fixed-size integers) or serious inefficiency (Python has no overflow, but multiplying huge numbers is still slow). Per [[Modular Arithmetic - Overview]], taking the modulus **at every multiplication step** produces the identical final answer while keeping every intermediate value small.

## Naive code (correct in theory, unsafe/slow in practice)
```python
class Solution:
    def maximumProduct(self, nums: List[int], k: int) -> int:
        heapq.heapify(nums)

        for _ in range(k):
            heapq.heappush(nums, heapq.heappop(nums) + 1)

        MOD = 1_000_000_007
        ans = 1
        for x in nums:
            ans *= x

        return ans % MOD
```
This risks Time Limit Exceeded or an outright wrong answer in languages where fixed-size integer types (e.g. `long long`) can't hold the full product before the final `% MOD`.

## Fixed code — modulus applied at every step
```python
class Solution:
    def maximumProduct(self, nums: List[int], k: int) -> int:
        heapq.heapify(nums)

        for _ in range(k):
            heapq.heappush(nums, heapq.heappop(nums) + 1)

        MOD = 1_000_000_007
        ans = 1
        for x in nums:
            ans = (ans * x) % MOD

        return ans
```
Only the multiplication loop changes — `ans` is kept bounded by `MOD` throughout, never allowed to grow unbounded.

## Complexity
`k` heap operations, each **O(log n)** (`n = len(nums)`) → **O(k log n)**. Final product computation: **O(n)**. **Total: O((n + k) log n) time** (heap size bounded by `n` throughout). **Space: O(n)** for the heap.

#dsa #algorithms #modular-arithmetic #heaps #greedy

Related: [[Modular Arithmetic - Overview]], [[Heaps - Overview]], [[Greedy Algorithms - Overview]]
