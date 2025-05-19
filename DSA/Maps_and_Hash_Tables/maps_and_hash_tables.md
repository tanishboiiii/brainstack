# Maps, Hash Tables, and Skip Lists

## Maps and Dictionaries:

Python's **dict** class represents an abstraction known as a dictionary, in which unique **keys** are mapped to associated **values**. They are also commonly known as **associative arrays** or **maps**.

An example, illustrates a map from the names of countries to their associated units of currency:

| Country | Currency |
| --- | --- |
| Turkey | Lira |
| Spain | Euro |
| Greece | Euro |
| China  | Yuan |
| United States  | Dollar |
| India | Rupee |

**Note:** The keys (country names) are assumed to be unique, but the values (currency units) are not necessaily unique. Unlike a stadard array, indices for a map need to be consecutive nor even numeric.

The map may be implemented so that a search for a key, and its associated value can be preformed very efficiently, thereby supporting fast lookup in such applications.

### The Map ADT:

Signifigant behaviors of a map *M*:

| Syntax | Behaviour |
| --- | --- |
| `M[K]` | Return the value `v` associated with a key `k` in map `M`, if one exists; otw raise a `KeyError`. |
| `M[k] = v` | Associate value `v` with a key `k` in map `M`, replacing the existing value if the map already contains an item with key equal to `k`. |
| `del M[k] ` | Remove from map `M` the item with key equal to `k`; if `M`has no such item, then raise a `KeyError`. |
| `len(M)` | Return the number of items in map `M`. |
| `iter(M)` | The defualt iteration for a map generates a sequence of *keys* in the map. It allows for a loop of the form, `for k in M`. |

### Counting Word Frequencies:

*Goal:* Count how many times each word appears in a document.

Key Concepts:
- Use a dictionary (map) to store: `{word: count}`.
- Ignore punctuation and non-alphabetic characters.
- Covert entire document to lowercase
- Split into words using the `.split()` on white space.

```.py
freq = {}
for piece in open(filename).read().lower().split():
    word = ''.join(c for in c in piece if c.isalpha()) # only conider aplhabetic characters within this piece
    if word: # require atleast one alphabetic character
        freq[word] = 1 + freq.get(word, 0) # increment count in dict
```

With this you can now look through `freq` dictionary to find word frequency, ex. max word frequency

## Hash Tables

A hash table is a fundemental data structure for implementing a **map (or dictionary)**. Python's built in `dict` is based on a hash table. It allows fast-access to data  using keys via syntax like `M[k]`.

Conceptual Warm-up:
- Imagine keys are integers in the range `0` to `N-1`, for some large `N`
- We can represent the map using a lookup table (array) of length `N`, where the index corresponds to the key.
- Example: A lookup tabe of length 11 storing (1,D), (3,Z), (6,C), (7,Q). Values would be stored directly at the index corresponding to the key.

![alt text](image.png)

- Operations like `__get__item`, `__setitem__`, and `__delitem__` can be done in *O(1)* worst-case time in this setup.

**Limitations of Direct Lookup Table:**
1. Storage inefficiency if `N >> n` there is too much unused space.
2. Keys in maps are not necessarily integers.

**Solution? (Hash Tables):**
- Use a hash function to map any key to an integer index in `[0, N-1]`.
- Goal: Distribute keys evenly across the array to avoid clustering.
- Resulting structure bucket array. (Figure coming...)

**Collisions and Buckets:**
- Different keys may hash to the same index -> this is a collision.
- Resolve collisions by having buckets at each index.
    - Each bucket is a collection (eg a list or linked lists of key-value pairs)
    - Example: Bucket at index 4 holds [(25, C), (3, F), (14, Z)]

![alt text](image-1.png)

## Hash Functions:


