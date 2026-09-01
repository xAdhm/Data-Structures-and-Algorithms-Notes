# Complexity Cheatsheet - Sorting Algorithms

Every major language has a built-in sort. Safe default assumption: sorting costs **O(n log n)**, where `n` = number of elements. (The specific algorithm behind a language's built-in sort varies — e.g. Python uses Timsort; C++ doesn't mandate a specific algorithm.)

## Stable sort
A sort is **stable** if, for two elements with equal keys/values, their **relative order from the original list is preserved** in the sorted output — if `R` appeared before `S` originally (and they're "equal" by the sort key), `R` still appears before `S` after sorting.

#dsa #algorithms #big-o #reference

Related: [[Complexity Cheatsheet - By Data Structure]], [[Complexity Cheatsheet - Input Size Guide]]
