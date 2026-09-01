# Code Templates - Quick Reference

A consolidated cheat sheet of code templates for every pattern covered in the course. Meant for quick lookup/copy-paste during practice or interviews, not for deep study — see the pattern-specific notes for explanations of *why* each template works.

**Note:** two topics appear here for the first time — **Tries** and **Dijkstra's algorithm** — neither has a dedicated concept note yet in this vault; these templates are included for completeness/reference until a full article on them is covered.

## Two Pointers — one input, opposite ends
See [[Two Pointers - Converging Pointers Method]].
```python
def fn(arr):
    left = ans = 0
    right = len(arr) - 1
    while left < right:
        # do some logic here with left and right
        if CONDITION:
            left += 1
        else:
            right -= 1

    return ans
```

## Two Pointers — two inputs, exhaust both
See [[Two Pointers - Two Iterables Method]].
```python
def fn(arr1, arr2):
    i = j = ans = 0
    while i < len(arr1) and j < len(arr2):
        # do some logic here
        if CONDITION:
            i += 1
        else:
            j += 1

    while i < len(arr1):
        # do logic
        i += 1

    while j < len(arr2):
        # do logic
        j += 1

    return ans
```

## Sliding Window
See [[Sliding Window - Dynamic Window Size]].
```python
def fn(arr):
    left = ans = curr = 0
    for right in range(len(arr)):
        # do logic here to add arr[right] to curr
        while WINDOW_CONDITION_BROKEN:
            # remove arr[left] from curr
            left += 1
        # update ans

    return ans
```

## Build a Prefix Sum
See [[Prefix Sum - Overview]].
```python
def fn(arr):
    prefix = [arr[0]]
    for i in range(1, len(arr)):
        prefix.append(prefix[-1] + arr[i])

    return prefix
```

## Efficient String Building
See [[String Building - O(n) Technique]]. (Note: in JavaScript, benchmarking shows `+=` concatenation is actually faster than `.join()`, unlike the Python/general guidance.)
```python
# arr is a list of characters
def fn(arr):
    ans = []
    for c in arr:
        ans.append(c)

    return "".join(ans)
```

## Linked List — Fast and Slow Pointer
See [[Fast and Slow Pointers - Overview]].
```python
def fn(head):
    slow = head
    fast = head
    ans = 0
    while fast and fast.next:
        # do logic
        slow = slow.next
        fast = fast.next.next

    return ans
```

## Reversing a Linked List
See [[Linked Lists - Reversing a Linked List]].
```python
def fn(head):
    curr = head
    prev = None
    while curr:
        next_node = curr.next
        curr.next = prev
        prev = curr
        curr = next_node

    return prev
```

## Find Number of Subarrays That Fit an Exact Criteria
See [[Hashing - Subarray Sum Equals K (Exact Constraint Pattern)]].
```python
from collections import defaultdict

def fn(arr, k):
    counts = defaultdict(int)
    counts[0] = 1
    ans = curr = 0
    for num in arr:
        # do logic to change curr
        ans += counts[curr - k]
        counts[curr] += 1

    return ans
```

## Monotonic Increasing Stack
See [[Monotonic Stacks and Queues - Overview]]. (Same logic applies to a monotonic queue — flip `>` to `<` for monotonic decreasing.)
```python
def fn(arr):
    stack = []
    ans = 0
    for num in arr:
        # for monotonic decreasing, just flip the > to <
        while stack and stack[-1] > num:
            # do logic
            stack.pop()
        stack.append(num)

    return ans
```

## Binary Tree — DFS (recursive)
See [[Binary Trees - DFS Overview]].
```python
def dfs(root):
    if not root:
        return

    ans = 0
    # do logic
    dfs(root.left)
    dfs(root.right)
    return ans
```

## Binary Tree — DFS (iterative)
See [[Binary Trees - Iterative DFS]].
```python
def dfs(root):
    stack = [root]
    ans = 0
    while stack:
        node = stack.pop()
        # do logic
        if node.left:
            stack.append(node.left)
        if node.right:
            stack.append(node.right)
    return ans
```

## Binary Tree — BFS
See [[Binary Trees - BFS Overview]].
```python
from collections import deque

def fn(root):
    queue = deque([root])
    ans = 0
    while queue:
        current_length = len(queue)
        # do logic for current level
        for _ in range(current_length):
            node = queue.popleft()
            # do logic
            if node.left:
                queue.append(node.left)
            if node.right:
                queue.append(node.right)
    return ans
```

## Graph — DFS (recursive)
See [[Graphs - DFS Implementation Differences from Trees]]. Assumes nodes numbered `0` to `n-1`, graph given as an adjacency list — convert other input formats first (see [[Graphs - Input Formats]]).
```python
def fn(graph):
    def dfs(node):
        ans = 0
        # do some logic
        for neighbor in graph[node]:
            if neighbor not in seen:
                seen.add(neighbor)
                ans += dfs(neighbor)

        return ans

    seen = {START_NODE}
    return dfs(START_NODE)
```

## Graph — DFS (iterative)
```python
def fn(graph):
    stack = [START_NODE]
    seen = {START_NODE}
    ans = 0
    while stack:
        node = stack.pop()
        # do some logic
        for neighbor in graph[node]:
            if neighbor not in seen:
                seen.add(neighbor)
                stack.append(neighbor)

    return ans
```

## Graph — BFS
See [[Graphs - BFS Overview]].
```python
from collections import deque

def fn(graph):
    queue = deque([START_NODE])
    seen = {START_NODE}
    ans = 0
    while queue:
        node = queue.popleft()
        # do some logic
        for neighbor in graph[node]:
            if neighbor not in seen:
                seen.add(neighbor)
                queue.append(neighbor)

    return ans
```

## Find Top K Elements with Heap
See [[Heaps - Top K Pattern]].
```python
import heapq

def fn(arr, k):
    heap = []
    for num in arr:
        # do some logic to push onto heap according to problem's criteria
        heapq.heappush(heap, (CRITERIA, num))
        if len(heap) > k:
            heapq.heappop(heap)

    return [num for num in heap]
```

## Binary Search
See [[Binary Search - Overview]].
```python
def fn(arr, target):
    left = 0
    right = len(arr) - 1
    while left <= right:
        mid = (left + right) // 2
        if arr[mid] == target:
            # do something
            return
        if arr[mid] > target:
            right = mid - 1
        else:
            left = mid + 1

    # left is the insertion point
    return left
```

## Binary Search — Duplicates, Leftmost Insertion Point
See [[Binary Search - Handling Duplicates]].
```python
def fn(arr, target):
    left = 0
    right = len(arr)
    while left < right:
        mid = (left + right) // 2
        if arr[mid] >= target:
            right = mid
        else:
            left = mid + 1
    return left
```

## Binary Search — Duplicates, Rightmost Insertion Point
```python
def fn(arr, target):
    left = 0
    right = len(arr)
    while left < right:
        mid = (left + right) // 2
        if arr[mid] > target:
            right = mid
        else:
            left = mid + 1
    return left
```

## Binary Search — For Greedy Problems
See [[Binary Search - On Solution Spaces]] and [[Binary Search - Min vs Max Answer Implementation]].

**Looking for a minimum:**
```python
def fn(arr):
    def check(x):
        # this function is implemented depending on the problem
        return BOOLEAN
    left = MINIMUM_POSSIBLE_ANSWER
    right = MAXIMUM_POSSIBLE_ANSWER
    while left <= right:
        mid = (left + right) // 2
        if check(mid):
            right = mid - 1
        else:
            left = mid + 1

    return left
```

**Looking for a maximum:**
```python
def fn(arr):
    def check(x):
        # this function is implemented depending on the problem
        return BOOLEAN
    left = MINIMUM_POSSIBLE_ANSWER
    right = MAXIMUM_POSSIBLE_ANSWER
    while left <= right:
        mid = (left + right) // 2
        if check(mid):
            left = mid + 1
        else:
            right = mid - 1

    return right
```

## Backtracking
See [[Backtracking - Overview]].
```python
def backtrack(curr, OTHER_ARGUMENTS...):
    if (BASE_CASE):
        # modify the answer
        return

    ans = 0
    for (ITERATE_OVER_INPUT):
        # modify the current state
        ans += backtrack(curr, OTHER_ARGUMENTS...)
        # undo the modification of the current state

    return ans
```

## Dynamic Programming — Top-Down Memoization
See [[Dynamic Programming - Framework]].
```python
def fn(arr):
    def dp(STATE):
        if BASE_CASE:
            return 0

        if STATE in memo:
            return memo[STATE]

        ans = RECURRENCE_RELATION(STATE)
        memo[STATE] = ans
        return ans

    memo = {}
    return dp(STATE_FOR_WHOLE_INPUT)
```

**Converting top-down → bottom-up** (full explanation in [[Dynamic Programming - Framework]]):
1. Initialize a `dp` array sized according to the state variables (e.g. state `(i, k)` → 2D array of size `len(nums) × k`), so `dp(4, 6)` becomes `dp[4][6]`.
2. Set base cases the same as in the top-down function (often just array-initialization defaults).
3. Write `for` loop(s) over the state variables (nested if multiple), iterating from base cases toward the answer state.
4. Each innermost-loop iteration = one top-down function call for that state — copy the logic in, replacing `dp(...)` calls with `dp[...]` array accesses.
5. Return `dp[...]` (the target state) instead of calling `dp(...)`.

## Build a Trie
Not yet covered in a dedicated note.
```python
# note: using a class is only necessary if you want to store data at each node.
# otherwise, you can implement a trie using only hash maps.
class TrieNode:
    def __init__(self):
        # you can store data at nodes if you wish
        self.data = None
        self.children = {}

def fn(words):
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

## Dijkstra's Algorithm
Not yet covered in a dedicated note. Finds shortest paths from `source` to every other node in a weighted graph.
```python
from math import inf
from heapq import *

distances = [inf] * n
distances[source] = 0
heap = [(0, source)]
while heap:
    curr_dist, node = heappop(heap)
    if curr_dist > distances[node]:
        continue

    for nei, weight in graph[node]:
        dist = curr_dist + weight
        if dist < distances[nei]:
            distances[nei] = dist
            heappush(heap, (dist, nei))
```

#dsa #algorithms #reference #templates

Related: [[Binary Search - Overview]], [[Backtracking - Overview]], [[Dynamic Programming - Framework]], [[Graphs - BFS Overview]], [[Heaps - Top K Pattern]]
