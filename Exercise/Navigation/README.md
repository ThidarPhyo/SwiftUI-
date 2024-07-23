# [Navigation](https://developer.apple.com/documentation/swiftui/navigation)

The following three navigation options are available on iOS.
* NavigationSplitView
* NavigationStack
* TabView

Of these, this section describes `NavigationStack` and `TabView`, which are frequently used in iOS development.

## NavigationStack

NavigationStack is a screen transition that stack screen horizontally.

* Reference : [UINavigationController](https://developer.apple.com/documentation/uikit/uinavigationcontroller)

## How to implement

An example code that uses NavigationStack to transition from the parent screen(RootView) to a child screen (DetailView) is shown below.
When NavigationStack is used, the NavigationBar is displayed in the NavigationBar can be used to return to the original screen, so only the code to transition to the next screen needs to be implemented and the code implementation to return is Basically, this is unnecessary.

```swift
// ParentView
struct RootView: View {
    var body: some View {
        NavigationLink("Show Detail") {
            DetailView(message: "Hello")
        }
    }
}

// ChildView
struct DetailView: View {
    let message: String
    
    var body: some View {
        Text(message)
    }
}

struct MainView: View {
    
    var body: some View {
        NavigationStack {
            RootView()
        }
    }
}
```

If you want to control the screen transitions yourself instead of doing them automatically, use .navigationDestination(...) instead of NavigationLink.

* By `Bool` value:

```swift
// ParentView
struct RootView: View {
    
    @State var isPresented = false
    
    var body: some View {
        Button("Show Detail") {
            // When the button is pressed, just set 'isPresennted' to 'true'
            isPresented = true
        }
        // if 'isPresented == true', the screen transition will be performed.
        // if close the screen, 'isPresente' will be set to 'false'
        .navigationDestination(isPresented: $isPresented) {
            DetailView(message: "Hello")
        }
    }
}
```
* If want to pass any object to a chidlView

```swift
// ParentView
struct RootView: View {
    
    @State var item: String?
    
    var body: some View {
        Button("Show Detail") {
            // When the button is pressed, simply set 'item' to the value , to pass to the childView
            item = "Hello"
        }
        // If 'item != nil' the screen transition will be performed.
        // Set 'nil' to 'item' when cloase the screen.
        // If you set 'nil' to 'item' , it will close the screen.
        .navigationDestination(item: $item) {
            // '$0' is the value of 'item', Optional is out
            DetailView(message: $0)
        }
    }
}
```
