# String Building - O(n) Technique

Since strings are immutable in most languages (see [[Arrays and Strings - Overview]]), concatenating a single character onto a string is **O(n)** — the entire string has to be copied to build the new one.

## The naive trap: O(n²)
If you build a final string of length `n` one character at a time via concatenation, the cost at each step is 1, 2, 3, ..., n characters copied. Total operations = 1+2+...+n = n(n+1)/2 → **O(n²)**.

Simple repeated concatenation in an immutable-string language will always cost O(n²), even though the final result is only length n.

## The fix: build with a mutable structure, then convert once
The general pattern (language-dependent specifics below):
1. Use a mutable list/buffer, append characters to it — O(1) per append (amortized), O(n) total across n operations
2. Convert to a string once at the end — O(n)
3. Total: O(n + n) = O(2n) = **O(n)**

### Python
```
def build_string(s):
    arr = []
    for c in s:
        arr.append(c)

    return "".join(arr)
```

### JavaScript
```
let buildString = s => {
    let arr = [];
    for (let i = 0; i < s.length; i++) {
        arr.push(s[i]);
    }

    return arr.join("");
};
```

### Java
Use `StringBuilder`:
```
public string buildString(String s) {
    StringBuilder sb = new StringBuilder();
    for (int i = 0; i < s.length(); i++) {
        sb.append(s.charAt(i));
    }

    return sb.toString();
}
```

### C++
Strings are mutable, so plain `+=` is fine — no special technique needed.

**Takeaway:** know the idiomatic O(n) string-building approach for whatever language you're interviewing in — this comes up constantly whenever a problem asks you to build/return a string.

#dsa #algorithms #arrays #strings #big-o

Related: [[Arrays and Strings - Overview]], [[Arrays and Strings - Time Complexity of Operations]]
