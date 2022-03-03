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
- 
