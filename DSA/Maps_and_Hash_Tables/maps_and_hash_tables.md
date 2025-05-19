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

### Hash Functions:

**Hash Function:** A hash function *h*, maps each key *k* to an integer in the range *[0, N-1]*, where *N* is the capacity of the bucket array for a hash table.

The main idea is that with such a *hash function*, we use the hash function value *h(k)*, as an index into our bucket array, *A*, instead of the key*k*, That is we store the item *(k, v)* in the bucket *A[h(k)]*.

**Collision:** If there are two or more keys with the same hash value, then two different items will be mapped to the same bucket *A*. In this case, we say that a collision has occured.

Good hash functions minimize collisions and are fast to compute.

The hash function, *h(k)* is commonly broken down into a two part process.
1. Hash Code: Converts key to an integer.
2. Compression Function: Maps that integer to *[0, N-1]*

### Hash Codes:

We desire that the set of hash codes assigned to our keys should avoid collisions as much as possible (this is because if the hash codes of our keys cause collisions, then there is no hope for our compression function to avoid them).

Bit Interpretation:
- Keys (eg. 314, 3.14, etc) can be interpreted as integers from their binary represnetation.
- For longer keys, compress high and low 32 bits, using exculusive or, or summing and ignoring overflow.
- Bit interpretation is not the best hash code approach as it causes lots of unwanted collisions for common groups of strings. Notice that it doesn't really take into account the ordering of characters thus using this function would result in collisions for `stop`, `tops`, `pots`, etc. A better hash code should take into consideration the position of the $x_i$'s.

Polynomial Hash Code:
- Treat key as a tuple of components (eg. characters) and compute:
$$x_0a^{n-1} + x_1a^{n-2} + ... + x_{n-2}a + x_{n-1}$$ 
- Multiplies each component by a power of constant *a* (commonly 33, 37, 39, or 41).
- Helps reduce clustering and distrubtes values well. This should be intuitive since multiplication by different powers is used as a way to spread out the influence of each component across the resulting hash code.

Cyclic-Shift Hash Codes:
- 
