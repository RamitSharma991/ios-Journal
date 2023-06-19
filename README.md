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




Live Activities are an Immersive, glanceable way to keep track of an event or the progress of a task. They have a discrete start and end and provides real-time updates from background app on runtime or remotely using Push Notifications.

## Live Activity overview

* Declarative programmatic layout with SwiftUI and WidgetKit.
* Explicit user action to begin a Live Activity.
* A Live Activity can be requested when your app is in the foreground. 
* Live Activities are user-moderated similar to Notifications.
* Someone can easily dismiss or turn them off for your app altogether.
* Must support Lock Screen and the Dynamic Island. 
* Update remotely using push notifications.
* Dynamic Island displays Live Activities throughout the system when the app is in the background. 
* When one Live Activity is active, it’s rendered using its variable-width, “compact” presentation.
* The Dynamic Island displays up to two live activities at a time.
* One of these Live Activities appears attached to the TrueDepth camera, while the other renders in its own detached view.
* Both of these Live Activities use their “minimal” presentation.
* Long press a Live Activity to display its “expanded” presentation, giving even more glanceable information.
* In the expanded presentation, views can deep link to different areas within the app. 
* Relies on the ActivityKit framework, empowering apps to request, update, and manage their lifecycles.

### New experiences for Live Activities in iOS 17

* In addition to the Lock screen and Dynamic Island, Live Activities appear in StandBy.
* Now iPad supports Live Activities. 
* Interactive Live Activities 
   * Leverage widget enhancements
   * Add buttons or toggles


## Lifecycle of Live Activities

The Lifecycle of a Live Activity contains four main steps: 

* Request
* Update 
* Observe activity state
* End

## Building Live Activity UI

* Show most essential content
* Simple design
* Show additional details in the application

### Dynamic Island presentations.

 * There are three presentations: ***compact, minimal and expanded.***
 * When an app’s Live Activity is the only one running on the system, it’ll be displayed using the compact presentation.
 * The compact presentation has two areas, ***leading and trailing.***
 * They appear together to form a cohesive presentation in the Dynamic Island.
 * Choose essential content to show in the leading and trailing space.
 * Users should be able to identify the specific activity by looking at the content here.
 * Create a DynamicIsland view builder to represent each of those presentations. 
 * When more than one app starts a Live Activity, the system chooses which Live Activities are visible and displays both of them using the minimal presentation for each: one minimal presentation appears attached to the Dynamic Island while the other appears detached.
 * Your minimal view should only have the most critical information, as you have very limited space to work with.
 * When users touch and hold a Live Activity in a compact or minimal presentation, the system displays the content in an expanded presentation.
 * For the expanded presentation, the system divides the expanded presentation into different areas. 
 * The first closure of the DynamicIsland view builder represents the expanded content. 
 * Within that closure, each section content can be defined with the expanded region passing the specific position.



## Related Sessions

- https://developer.apple.com/wwdc23/10028
- https://developer.apple.com/wwdc23/10185
- https://developer.apple.com/wwdc23/10194



























```swift

}
```

