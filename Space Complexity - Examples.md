# Space Complexity — Worked Examples

**Rule:** never count space used by the input (don't modify input — bad practice), and usually don't count space used by the output/answer unless explicitly asked.

## O(1) — constant space
```
for (int num: arr) {
    print(num)
}
```
Only allocates a single int `num` — doesn't grow with n.

## O(n) — linear space
```
Array doubledNums = int[]
for (int num: arr) {
    doubledNums.add(num * 2)
}
```
`doubledNums` ends up storing n integers.

## Still O(n) even with a fraction of n
```
Array nums = int[]
int oneHundredth = n / 100
for (int i = 0; i < oneHundredth; i++) {
    nums.add(arr[i])
}
```
Storing n/100 elements → O(n/100) → constant dropped → **O(n)**.

## O(n·m) — 2D allocation
```
Array grid = int[n][m]
for (int i = 0; i < arr.length; i++) {
    for (int j = 0; j < arr2.length; j++) {
        grid[i][j] = arr[i] * arr2[j]
    }
}
```
Grid has dimensions n × m → **O(n·m)**.

#dsa #algorithms #big-o #space-complexity

Related: [[Big O - Rules for Calculating Complexity]], [[Time Complexity - Examples]]
