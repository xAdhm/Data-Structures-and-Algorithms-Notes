# Recursion - Call Stack and Execution Order

With iteration, execution order is simple: top to bottom, line by line. With recursion, it's less obvious because calls cascade — each call "waits" while a new one runs, then resumes where it left off.

## Example: print 1 to 3, with a line after the recursive call

```
function fn(i):
1.  if i > 3:
2.    return

3.  print(i)
4.  fn(i + 1)
5.  print(f"End of call where i = {i}")
6.  return

fn(1)
```

Output:
```
1
2
3
End of call where i = 3
End of call where i = 2
End of call where i = 1
```

## Why this happens
- `fn(1)` prints `1`, then calls `fn(2)` (line 4). `fn(1)` is now paused, waiting on `fn(2)`.
- `fn(2)` prints `2`, then calls `fn(3)`. `fn(2)` is paused.
- `fn(3)` prints `3`, then calls `fn(4)`. `fn(3)` is paused.
- `fn(4)` hits the base case (`i > 3`) and returns immediately.
- Control returns to `fn(3)` right after its line 4 call — so it runs line 5: `"End of call where i = 3"`, then returns.
- Control returns to `fn(2)` after its line 4 call — runs line 5: `"End of call where i = 2"`, then returns.
- Same for `fn(1)` → `"End of call where i = 1"`, then the whole thing terminates.

**Key idea:** the *print-before-recursing* lines (line 3) execute in forward order (1, 2, 3), while the *print-after-recursing* lines (line 5) execute in reverse order (3, 2, 1) — because each call has to fully finish (including everything after its recursive call) before control returns to its caller.

## Local scope per call
Each function call has its own local scope. In the example above, while `fn(3)` is active, there are simultaneously 3 separate "versions" of `i`: `i = 1` (in `fn(1)`'s scope), `i = 2` (in `fn(2)`'s scope), `i = 3` (in `fn(3)`'s scope). Modifying `i` inside one call (e.g. `i += 1` inside `fn(3)`) only affects that call's own copy — the other calls' versions of `i` are unaffected.

#dsa #algorithms #recursion

Related: [[Recursion - Overview]], [[Recursion - Base Cases]]
