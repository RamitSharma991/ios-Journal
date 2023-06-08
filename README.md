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












## Web Apps features
- iOS17 and MacOS Sonoma fully support Home Screen web apps.
- Web apps on Mac work great with no adoption required by developers.
- Any website can become a web app. 
- Web apps on Mac are fully integrated with many of the features that you would expect from a native app on macOS.
- Like all Mac apps, web apps work great with Stage Manager, Mission Control, and keyboard shortcuts, such as command + tab.
- Web apps can be opened from the Dock, Launchpad, and Spotlight Search.
- Web apps work with AutoFill credentials from iCloud Keychain and from third-party apps that have adopted the Credential Provider Extension API.
- Add to Home Screen is now available in Safari View Controller.  
- We can create a web app by adding a website to the Dock from the File menu `File > Add to Dock`.


## Customising your Web Apps
When a webpage is added to the Dock on macOS, it is always treated as a web app. Furthermore : 
- We can control the initial behavior of the toolbar for the web app's window.
- We can customize the experience of the user through system permission prompts and in the Privacy & Security section of System Settings .
- The default behavior on iOS is different from macOS. 
- Websites that have been added to the Home Screen on iOS and iPadOS, with the standalone display mode, will become a Home Screen web app.
- Home Screen web apps have a standalone, app-like experience on iOS, with separate cookies and storage from the browser. 
- There's no browser-provided UI, such as a toolbar, and all the content is from the web page.
- If you want your site to be able to use Web Push and badging on iOS, then you should use the standalone display mode.
- To set the display mode add a web app manifest to the site. 
- The web app manifest is a way for a website to communicate its intended behavior for web app-related features with the system.
- To add a web app manifest to your website, simply add a link with `rel="manifest"` ,to a JSON file in the head of your HTML.
- In the corresponding manifest file, add the keys and values that apply to your website.
- Set the name of the web app.
- Then change the display mode, set display to `“standalone”`
- On macOS, the web app will not have a toolbar and on iOS and iPadOS, the site will open in a Home Screen web app.

#### Links clicked within the Web App when opened.
- All web apps have an associated scope. 
- Links within the scope open within the web app. 
- The default scope is the host of the webpage used to create the web app. 
- Refine the scope using the web app manifest to limit it to a specific path on your site.
- Any links within the scope will stay within the web app and any links outside the scope will open in the default browser. 
- For links in the scope to open in the default browser just adjust the scope in the web app manifest by adding the `"start_url"`. 
- Now add the scope. The scope is a subdirectory of the manifest URL.
- In Home Screen web apps on iOS, links outside the scope will open in Safari View Controller.


## Authentication best practices

- Use cookies for authentication state
- Ensure login flow stays within the web app
- OAuth implementation
- Emailed login links

## Notifications
- Standard based web push.
- Use application icons.
- Notification sound: 
  - iOS and iPadOS sound on by default and macOS sound off by default. 
  - If the notification should be silent, set `silent: true` in the options when requesting your notification. 
  - If the notification should make a sound, then set `silent: false`.
- just like for native app notifications, users can control notification sounds using notifications settings
- Badging:
  - Useful to alert users that there is something to address in the web app.
  - Badges can be updated when the web app is open and when push events are being handled in the background. 
  - Users can always configure badges in Settings.


## Focus 
- Home Screen web apps on iOS and web apps on Mac integrate with Focus to give users control over their notifications.
- Users can set which notifications they want to see in different Focus modes across all devices. 
- The `"id"` manifest key defines unique web apps within the same domain.
- Used for syncing Focus modes and can be useful if you have multiple parts of your website that should be treated as distinct web apps under the same domain.
- If you only have one web app for a given domain, then you don't need to set the id.
- The fallback if there is no id provided is the `start_url`.

### Focus syncing
- Focus modes sync across all of a user's devices.
- Both you and your users control how Focus mode settings are synced.
- Separate id keys of the web app manifest can be used in the wb apps.
- Focus modes sync across a user's device when the name and id align.
- Users can create multiple instances of a web app for a given site on their device.


## Related web app APIs
- User Activation API
- Fullscreen API
- Screen Orientation API








