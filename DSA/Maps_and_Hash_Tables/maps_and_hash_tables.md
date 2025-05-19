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




