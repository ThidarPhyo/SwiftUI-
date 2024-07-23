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
struct RootView: View {
    var body: some View {
        NavigationLink("Show Detail") {
            DetailView(message: "Hello")
        }
    }
}

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
