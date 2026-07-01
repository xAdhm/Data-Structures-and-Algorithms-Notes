# Arrays and Strings - Overview

Arrays (1D) and strings are very similar for algorithm purposes — both represent an **ordered group of elements**. Most algorithm problems involve one or the other as input, so being comfortable with their basic operations and common patterns is essential.

## "Array" means different things per language
- **Python:** primarily uses "lists" — lenient, no type or size declaration needed (`arr = []`)
- **C++:** raw arrays require a fixed size and data type at initialization; also has list-like support via `std::vector`
- Technically, a plain **array** can't be resized. A **dynamic array** (aka "list") can be. In algorithm problems, "array" almost always means *dynamic array* — this course (and most interview contexts) uses "array" loosely to mean dynamic array/list.

## Mutability
- **Mutable:** data that can be changed in place
- **Immutable:** data that cannot be changed — to "change" it, you must recreate it entirely

**Strings by language:**
- Python, Java → immutable
- C++ → mutable

### Why mutability matters
Given a mutable array `arr = ["a", "b", "c"]` and an immutable string `s = "abc"`, changing the `c` to `d`:
- Array: `arr[2] = "d"` — trivial, O(1)
- String: `s[2] = "d"` is not allowed — you must rebuild the entire string from scratch

For a short string this is irrelevant, but for a string with 100,000 characters, rebuilding it just to change one character costs **O(n)**, where n is the string length. This matters a lot for complexity analysis when a problem involves repeated string modification.

## Know your language
Array/string implementation details vary a lot by language (mutability, resizing behavior, etc.) — worth researching specifics for whichever language you're using in interviews.

#dsa #algorithms #arrays #strings

Related: [[Arrays and Strings - Time Complexity of Operations]]
