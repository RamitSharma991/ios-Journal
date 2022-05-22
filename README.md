# ios-Journal


1. Swift Alorithms and Collection Packages.
- Map: Makes loops faster and clearer. It provides extra context that the body of the closure, regardless of its length or complexity, is just transforming the input. Using map also makes this code faster because it avoids intermediate allocations due to array resizing by reserving capacity which raw loops don't bother doing.
- Compact Map: A map and filter algorithm that collects and iterates data, filtering out nils and mapping to unwrap optionals
- FlatMap: it joins together all the inner arrays into a single, flat collection of elements. This pattern of mapping and joining is so common that we define another special kind of map for it: flatMap. 
- Chaining together Algorithms: conscise, flexible and clearer code
- Lazy Algorithms and lazy adapters: FlattenSequence is a lazy adapter, a free to create thin wrapper processes elements on demand rather than doing all the work up front. They enable algorithm chains to have competitive performance with raw for loops. You just have to add a .lazy to the start of the chain and it makes any of the algorithms that take a closure, like map and filter, lazy. Lazy algorithm chains are a great fit for use cases where you're only processing a small number of elements from a potentially very large collection. When you need an array you can always just wrap your algorithm chain in an array initializer. 
- windows(ofCount:) : provides a sliding window into the elements of a collection. For each turn of the loop, window is just a subsequence of the base collection.
- adjacentPairs: vends a tuple rather than a subsequence, allowing for more convenient element access. 
- chunks(ofCount:) : chunks don't overlap. If a collection isn't evenly divisible by the chunk count, the last chunk in the sequence will contain the remainder. Just like windows, chunks are subsequences of the base collection, so they're cheap to create.
- isPrime: we'll iterate the chunks of consecutive elements that return the same value for isPrime. For convenience, chunked(on:) vends a tuple of both the chunk and the value being chunked on. 
- Data structures: the Swift standard library implements just three major general-purpose data structures: it provides arrays, unordered sets, and unordered dictionaries. These have proved great choices as universal collection types, and they're especially nice for transferring data across module boundaries. These happen to be new variations of the three standard collection types. We have a double-ended queue, an OrderedSet, and an OrderedDictionary. These are similar to array, set, and dictionary; they are variants of the same theme, adding new features to the existing constructs. That said, these new types aren't replacements for the existing ones; they are complementary to them. 
- Ordered Dictionary:  
The third data structure provided by the Collections package is an ordered analogue of the standard dictionary type. Like the standard dictionary, this is a sequence of key-value pairs that lets us use a key as a subscript to quickly look up its corresponding value. Unlike the regular dictionary, the order of key-value pairs is well-defined. By default, it follows the order in which the keys were originally inserted. To append a new element, we can assign a value to a new key. We can remove elements by assigning nil to an existing key. Throughout these operations, the ordered dictionary maintains its contents in a well-defined order.
Ordered dictionaries use array-like integer indices, but this introduces an interesting issue. In our example dictionary, the indexing subscript operation conflicts with the key subscript. When we subscript with zero, do we mean to access the value for the key zero or do we mean to retrieve the key-value pair at offset zero? We think that the key-based subscript is the primary operation for a dictionary type, so to prevent this ambiguity, subscripting an ordered dictionary always means the keying subscript. OrderedDictionary doesn't provide an indexing subscript operation at all. This means that OrderedDictionary cannot be a collection, because the collection protocol requires such a subscript. Therefore, OrderedDictionary only conforms to the sequence protocol. However, for cases where a collection conformance is desirable, OrderedDictionary provides the special elements view. Elements is a random-access collection that provides an indexing subscript returning a key-value pair. Looking at the underlying implementation, while the regular dictionary type uses two separate hash tables for storing keys and values respectively, an ordered dictionary uses a single compressed hash table and two parallel arrays instead. This can save even more space than ordered sets do. 
2.

