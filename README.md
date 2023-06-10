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
- Set the name of the web app and change the display mode, set display to `“standalone”`
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
- Just like for native app notifications, users can control notification sounds using notifications settings
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
- The fallback if there is no id provided is the `start_url`

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


















Web Inspector is part of Safari on macOS, and it provides a powerful set of tools that allow you to inspect all the resources and activities of a website, web app, web extension, or home screen web app.Many improvements have been made to developer features in Safari, including a streamlined way to pair and inspect web content on devices, a quick way to open a web page in a Simulator, a refreshed Responsive Design Mode, and many others. To enable Web inspector: 

- Open the Settings window of Safari and switch to the Advanced tab. 
- At the bottom, you'll find the setting to "Show features for web developers.
- Click the checkbox to enable this. The Develop menu is now available in the menu bar.
- Open Web Inspector using the menu item called Show Web Inspector or by pressing the keyboard shortcut Option+Command+I on any web page.



## Typography inspection

Web Inspector can help with a host of typography inspection tools. You can find them in the Details sidebar of the Elements tab, in the Font panel. 

 - It shows properties and capabilities of the font used on the selected element, such as the name of the primary font used. 
 - Reference this to quickly check if the font you expected was indeed used. 
 - This only identifies the primary font.
 - If the selected node includes characters for which the primary font does not have glyphs, a fallback font will be used for those.
 - Font panel shows a summary of the basic font properties, like font size, style, weight, and stretch.
 - There's also a section that shows the supported font feature properties and their used values. 
 - These toggle special aspects of a typeface such as ligatures, small caps instead of lowercase characters, special numeric styles, and many others, depending on what the font supports. 
 - Now the Font panel shows warnings for synthetic bold or oblique styles. Often, these aren't slanted versions of the upright style, but instead they're cursive, specially designed to convey a particular aesthetic. Something similar happens for synthetic bold, where the stroke of the glyphs is made artificially thicker. 
 - Web Inspector now displays a warning when a synthetic bold or oblique is used. 
 - It shows up next to the synthesized weight or style in the basic properties section of the Font panel. 
 - This warning can be a hint that the expected font file was not loaded. 
 - Variable fonts can help when the font file just doesn't support the exact values you asked for. 
 - All aspects of a variable font that can be configured are expressed as variation axes. 
 - Web Inspector can help here. When you inspect an element that uses a variable font, the Font panel shows you a list of the supported variation axes. For each, it shows its axis tag-- a four-character identifier-- an optional axis label, the supported minimum and maximum values, as well as the current value, or the default value if one is not specified in CSS.
 - Interactive controls to edit the values of variation axes and see the results live on the inspected page.To integrate these changes back into my project, I can copy the new CSS properties from the Styles panel or from the Changes panel.


## User preference overrides 

There's a new tool in Web Inspector to emulate user preferences. Click the new icon in the Elements tab to reveal the User Preference Overrides popover. Here, you'll find a set of toggles to override user preferences just for the inspected page while Web Inspector is open. These preferences map to CSS media features which you can use to adapt the style and behavior of your web page. Some examples are these overrides are of the preference for color scheme maps to the prefers-color-scheme media feature in CSS and to override the preference for reduced motion.  


## Element badges 

- In the node tree view of the Elements tab, you can already see badges next to elements that act as CSS Flex or CSS Grid containers. Element badges provide a quick way to identify at a glance nodes of particular interest. In this case, nodes that create a CSS Grid or Flex layout context. 
`<element> grid`   `<element> flex`
- One of the trickiest CSS layout issues to debug is unwanted scroll, like a container that scrolls horizontally because the content inside it doesn't fit the available width. The new element badge `<element> Scroll` that helps to identify unwanted scroll.
- It provides a quick visual hint in the node tree when an element's content overflows its bounds and a scroll bar is applied.
- A new Event badge appears next to elements which have JavaScript event listeners attached to them. It works both for built-in events, like pointer or UI events, as well as custom JavaScript events that you dispatch in your code.
  
## Breakpoint enhancements
- When debugging JavaScript, you may be used to adding `console.log()` statements to your code. Breakpoints, on the other hand, are a powerful way to debug by pausing and stepping through JavaScript without having to make changes to your source.
- The easiest way to start is by clicking on a line number on a script file in the gutter of the Sources tab. 
- This sets a JavaScript breakpoint on that line of the script. Next time that line is about to run, Web Inspector will instead pause JavaScript execution at that point. While paused, you can observe the call stack, inspect the state of objects and variables in scope, and even make changes to them through the Console.
- You can resume JavaScript execution, or you can step through the code one expression at a time, using the stepping controls at the top. You can configure a breakpoint by right clicking on it and selecting Edit Breakpoint.
- There are many options you can set to control when the breakpoint is hit and even run actions when it does.
- You can control when a breakpoint is hit by setting a condition for it. This evaluates as JavaScript in the same scope where your breakpoint is set.
- You can also run actions when a breakpoint is hit, like evaluating a piece of JavaScript. 
- This runs in the same scope where the breakpoint is set. 
- You can use this to modify the state of your script before continuing. 
- You can also log messages to the console with expressions that have access to the state of variables and objects at the moment when JavaScript was paused. This is similar to adding a console.log() statement to your code, but without having to modify your source. Instead of logging variables and objects to the console, you can also use the Probe Expression action. This allows you to inspect the state of the given expression in the details sidebar panel of the Sources tab.

### Symbolic breakpoints
Symbolic breakpoints have been added  to pause before a function is about to be invoked. They are helpful to debug calls to built-in JavaScript functions or to pause in multiple functions with the same name.

If you want to learn more about these and the many other features you can use, go to webkit.org to find in-depth blog posts and documentation.


