# Time Complexity — Worked Examples

## Single loop → O(n)
```
for (int num: arr) {
    print(num)
}
```
Each iteration is O(1), loop runs n times → O(n).

## Loop with large constant inner loop → O(n)
```
for (int num: arr) {
    for (int i = 0; i < 500000; i++) {
        print(num)
    }
}
```
Inner loop is O(500,000) = O(1) (constant, doesn't depend on n). Outer loop runs n times → O(n).
Note: technically same complexity as the example above, but *practically* much slower — worth mentioning the gap between theory and practice in an interview.

## Nested loop over same array → O(n²)
```
for (int num: arr) {
    for (int num2: arr) {
        print(num * num2)
    }
}
```
Inner loop = O(n), runs for each of n outer iterations → O(n·n) = O(n²).

## Sequential (not nested) loops, two inputs → O(n + m)
```
for (int num: arr) { print(num) }
for (int num: arr) { print(num) }
for (int num: arr2) { print(num) }
```
First two loops: O(n) each. Third loop: O(m). Total = O(2n + m) = **O(n + m)** (constant 2 dropped, but n and m are different variables so neither term dominates the other — both stay).

## Triangular nested loop → O(n²)
```
for (int i = 0; i < arr.length; i++) {
    for (int j = i; j < arr.length; j++) {
        print(arr[i] + arr[j])
    }
}
```
Inner loop shrinks each pass: n + (n−1) + (n−2) + ... + 1 = n(n+1)/2 = (n² + n)/2 → drop lower-order term and constant → **O(n²)**.

## Logarithmic time — O(log n)
Means the input shrinks by a percentage at every step (not a fixed amount). Classic example: **binary search** — each step halves the search space (n → n/2 → n/4 → ...).
- Base of the log doesn't matter for Big O (all logs are related by a constant factor).
- `O(n log n)` is the complexity of efficient sorting algorithms — reasonably fast for most problems.

#dsa #algorithms #big-o #time-complexity

Related: [[Big O - Rules for Calculating Complexity]], [[Space Complexity - Examples]]
