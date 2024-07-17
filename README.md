# ViewModifier


## 概要
In SwiftUI, various modifiers such as font, foregroundColor, padding, and more are provided, but you can also create custom modifiers.

```swift
// ✅ Implement a ViewModifier
struct AppTextStyle: ViewModifier {
    
    // customizations View
    func body(content: Content) -> some View {
        content
            .font(.system(size: 14))
            .foregroundStyle(Color.appTextColor)
    }
}

struct ContentView: View {
    var body: some View {
        Text("Text")
            .modifier(AppTextStyle()) // Apply Modifier
    }
}
```

In practice, to avoid writing `modifier(AppTextStyle())` every time, it's common to define extensions like the following.

```swift
extension View {
    
    func appTextStyle() -> some View {
        modifier(AppTextStyle())
    }
}

struct ContentView: View {
    var body: some View {
        Text("Text")
            .appTextStyle()
    }
}
```
In that case, it's not much different from simply customizing a View using extensions.

```swift
extension View {
    
    func appTextStyle() -> some View {
        font(.system(size: 14))
            .foregroundStyle(Color.appTextColor)
    }
}
```

In SwiftUI, extensions cannot have properties like `@State` or `@Environment`. Therefore, it's preferable to use custom ViewModifiers when you need to use those features.

To summarize:

* Create a custom ViewModifier when using `@State` or `@Environment`.
* Use extensions for other cases.
