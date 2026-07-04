# Hashing - Python Hash Map Interface

Quick reference for the built-in Python dictionary (`dict`) — the language's [[Hashing - Hash Maps|hash map]] implementation.

## Declaration
```python
hash_map = {}
```
Or initialize with key-value pairs directly:
```python
hash_map = {1: 2, 5: 3, 7: 2}
```

## Checking if a key exists
Use the `in` keyword:
```python
1 in hash_map   # True
9 in hash_map   # False
```

## Accessing a value by key
Square brackets, same as array indexing:
```python
hash_map[5]   # 3
```

## Adding or updating a key
Also square brackets — behavior depends on whether the key already exists:
```python
hash_map[5] = 6    # key 5 exists -> value updated to 6
hash_map[9] = 15   # key 9 doesn't exist -> new pair inserted
```

## Deleting a key
```python
del hash_map[9]
```
⚠️ The key must exist, or this raises an error.

## Size
```python
len(hash_map)   # number of key-value pairs
```

## Iterating over keys
```python
keys = hash_map.keys()
for key in keys:
    print(key)
```

## Iterating over values
```python
values = hash_map.values()
for val in values:
    print(val)
```

## Iterating over key-value pairs together
```python
for key, val in hash_map.items():
    print(f"{key}: {val}")
```

## Worked mini-example
```python
my_hash_map = {}
my_hash_map[4] = 83
print(my_hash_map[4])        # 83
print(4 in my_hash_map)      # True
print(854 in my_hash_map)    # False

my_hash_map[8] = 327
my_hash_map[45] = 82523

for key, val in my_hash_map.items():
    print(f"{key}: {val}")
```

#dsa #algorithms #hashing #hash-map #python

Related: [[Hashing - Hash Maps]], [[Hashing - Sets]]
