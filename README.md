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







Enhance your iPad or iPhone app from a great app to one that feels at home on this new platform of Shared Space. Following are the key areas to focus.


# Interaction
- Interaction on this platform is fun and feels familiar. 
- One of the key components is the new natural input technique. 
- Tap allows people to look at a button, then tap their fingers together to interact.
- People can tap to toggle, tap, hold and swipe to interact with a slider, or tap a button.
- Direct touch requires reaching out to the app and touching the button in the space with one finger.
- Regardless of interaction method, the button provides continuous visual feedback to help with interaction accuracy.
- Hover effects exist on controls to inform where people are looking. 
- Controls that are inactive do not get hover effects. 
- If you're building custom controls, your hover effects may need some tuning.

### Tappable VStack with hover effect to the entire card available for interaction update and becomes tappable. 

```swift 
struct TappableCard: View {
   // Sample card
   var imageName = "BearsInWater"
   var headline = "Bear Fishing"
   var timeAgo = "42 Minutes ago"
   
   var body: some View {
      VStack {
         VStack(alignment: .leading) {
            Image(imageName)
               .resizable()
               .clipped()
               .aspectRatio(contentMode: .fill)
               .frame(width: 300, height: 250, alignment: .center)
            Text(headline)
               .padding([.leading])
               .font(.title2)
               .foregroundColor(.black)
         }
         Divider()
         HStack {
            HStack {
               Text(timeAgo)
                  .frame(alignment: .leading)
                  .foregroundColor(.black)
            }
            .padding([.leading])
            Spacer()
            VStack(alignment: .trailing) {
               Button { print("Present menu options") } label: {
                  Image(systemName: "ellipsis")
                     .foregroundColor(.black)
               }
            }
         }
         .padding(EdgeInsets(top: 5, leading: 5, bottom: 5, trailing: 5))
      }
      .frame(width: 300, height: 350, alignment: .top)
      .hoverEffect()
      .background(.white)
      .overlay(
         RoundedRectangle(cornerRadius: 10)
            .stroke(Color(.sRGB, red: 150/255, green: 150/255, blue: 150/255, opacity: 0.1), lineWidth: 3.0)
      )
      .cornerRadius(10)
      .onTapGesture {
         print("Present card detail")
      }
   }
}
```
### Custom player with the tap targets that are larger than hover effect bounds

```swift  
struct ContentView: View {
   var body: some View {
      VStack {
         // Video player
         HStack {
            Button { print("Going back 10 seconds") } label: {
               Image(systemName: "gobackward.10")
                  .padding(.trailing)
                  .contentShape(.hoverEffect, CustomizedRectShape(customRect: CGRect(x: -75, y: -40, width: 100, height: 100)))
                  .foregroundStyle(.white)
                  .frame(width: 500, height: 834, alignment: .trailing)
            }
            Button { print("Play") } label: {
               Image(systemName: "play.fill")
                  .font(.title)
                  .foregroundStyle(.white)
                  .frame(width: 100, height: 100, alignment: .center)
            }
            .padding()
            Button { print("Going into the future 10 seconds") } label: {
               Image(systemName: "goforward.10")
                  .padding(.leading)
                  .contentShape(.hoverEffect, CustomizedRectShape(customRect: CGRect(x: 0, y: -40, width: 100, height: 100)))
                  .foregroundStyle(.white)
                  .frame(width: 500, height: 834, alignment: .leading)
            }
         }
         .frame(
              minWidth: 0,
              maxWidth: .infinity,
              minHeight: 0,
              maxHeight: .infinity,
              alignment: .center
         )
      }
      .frame(
           minWidth: 0,
           maxWidth: .infinity,
           minHeight: 0,
           maxHeight: .infinity,
           alignment: .topLeading
      )
      .background(.black)
   }
}

struct CustomizedRectShape: Shape {
   var customRect: CGRect
   
   func path(in rect: CGRect) -> Path {
      var path = Path()
      
      path.move(to: CGPoint(x: customRect.minX, y: customRect.minY))
      path.addLine(to: CGPoint(x: customRect.maxX, y: customRect.minY))
      path.addLine(to: CGPoint(x: customRect.maxX, y: customRect.maxY))
      path.addLine(to: CGPoint(x: customRect.minX, y: customRect.maxY))
      path.addLine(to: CGPoint(x: customRect.minX, y: customRect.minY))
      
      return path
   }
}

```
- Hover effects on system controls work great; however, the ability to customize hover effects is powerful. 
- With the new hover effect API, apps can create hover effects for custom buttons, custom shapes, or even opt out of a control if necessary.



### Button with custom buttonStyle, then adding a lower effect to the button. 
```swift 
struct ContentView: View {
    var body: some View {
        VStack {
         Button("Howdy y'all") { print("🤠") }
            .buttonStyle(SixColorButton())
        }
        .padding()
    }
}

struct SixColorButton: ButtonStyle {
   func makeBody(configuration: Configuration) -> some View {
      configuration.label
         .padding()
         .font(.title)
         .foregroundStyle(.white)
         .bold()
         .background {
            // Background color bands
            ZStack {
               Color.black
               HStack(spacing: 0) {
                  // GREEN
                  Rectangle()
                     .foregroundStyle(Color(red: 125/255, green: 186/255, blue: 66/255))
                     .frame(width: 16)
                  // YELLOW
                  Rectangle()
                     .foregroundStyle(Color(red: 240/255, green: 187/255, blue: 64/255))
                     .frame(width: 16)
                  // ORANGE
                  Rectangle()
                     .foregroundStyle(Color(red: 225/255, green: 137/255, blue: 50/255))
                     .frame(width: 16)
                  // RED
                  Rectangle()
                     .foregroundStyle(Color(red: 200/255, green: 73/255, blue: 65/255))
                     .frame(width: 16)
                  // PURPLE
                  Rectangle()
                     .foregroundStyle(Color(red: 134/255, green: 64/255, blue: 151/255))
                     .frame(width: 16)
                  // BLUE
                  Rectangle()
                     .foregroundStyle(Color(red: 75/255, green: 154/255, blue: 218/255))
                     .frame(width: 16, height: 500)
               }
               .opacity(0.7)
               .rotationEffect(.degrees(35))
            }
         }
         .cornerRadius(10)
         .hoverEffect()
   }
}
```
### Honey comb app with custom shape buttons, then adding hover effects that clip to bounds of the honey comb shape.
```swift 
struct ContentView: View {
    var body: some View {
      VStack {
         Button { print("🐝") } label: {
            // Button label
            HoneyComb()
               .fill(.yellow)
               .frame(width: 300, height: 300)
               .contentShape(.hoverEffect, HoneyComb())
            }
         }
         .frame(width: 400, height: 400, alignment: .center)
         .background(.black)
         .padding()
      }
    }
}

struct HoneyComb: Shape {
   func path(in rect: CGRect) -> Path {
      var path = Path()
      path.move(to: CGPoint(x: rect.minX + (rect.width * 0.25), y: rect.minY))
      path.addLine(to: CGPoint(x: rect.maxX - (rect.maxX * 0.25), y: rect.minY))
      path.addLine(to: CGPoint(x: rect.maxX, y: rect.midY))
      path.addLine(to: CGPoint(x: rect.maxX - (rect.maxX * 0.25), y: rect.maxY))
      path.addLine(to: CGPoint(x: rect.minX + (rect.width * 0.25), y: rect.maxY))
      path.addLine(to: CGPoint(x: rect.minX, y: rect.midY))
      path.addLine(to: CGPoint(x: rect.minX + (rect.width * 0.25), y: rect.minY))
      return path
   }
}
```
- System controls that are disabled due to app state automatically do not get hover effects. 
- If apps want to de-emphasize specific interface elements, they can opt out individual items, they can opt out individual items. 
- Overriding hover effect ‘ .hoverEffectDisabled(Bool) ’ 
- The system accepts a maximum of two simultaneous inputs since each hand is a distinct touch.
- Custom gesture recognizers are also supported, but you may need to update them to run smoothly with the natural input expectations.

## Game Controllers Support 
  ### App Store indicator 
   -`GCSupportControllerUserInteraction`
   - Game controller capability 

# Visuals
- The system optimizes rendering, using dynamic content scaling so all images and text are always sharp at any angle, from any distance. 
- To provide the best experience, use vector-based content.  
- Prompts do not present modally. 

# Media 
- To ensure apps have an excellent capture experience, use `AVCaptureDevice` discovery session to confirm hardware availability.  
- Requesting permission before use is required. 
- Generalize your authorization prompt string to inform people of use, without mentioning specific hardware or software versions. 
- If no spatial persona is found on a device, then no camera frames will return to apps. 
  ## Media Playback
   - `AVRoutePickerView` and Picture in Picture are unavailable on this platform.
   - Apps that implement custom players need to check both availabilities before showing these controls.
   - Apps that utilize background audio will no longer get the background mode when the device is locked and will be fully suspended as this platform locks once removed. 
  ## Alternative media sources
   - Cloud-based media
   - Picker (document, photo)
   - VNDocumentCameraViewController








