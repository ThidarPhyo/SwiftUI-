# ViewModifier


## 概要
SwiftUI では font や foregroundColor, padding など様々な Modifier が用意されていますがカスタムの Modifier を作成することもできます。
```swift
// ✅ ViewModifier を実装するだけ
struct AppTextStyle: ViewModifier {
    
    // ここで View のカスタマイズを行う
    func body(content: Content) -> some View {
        content
            .font(.system(size: 14))
            .foregroundStyle(Color.appTextColor)
    }
}

struct ContentView: View {
    var body: some View {
        Text("Text")
            .modifier(AppTextStyle()) // Modifier を適用
    }
}
```

ただ実際は modifier(AppTextStyle()) と書く手間を省略するために次のように extension を用意することが多いです。

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
こうなると単に extension で View をカスタマイズするのとあまり変わりません。

```swift
extension View {
    
    // これでいいじゃん
    func appTextStyle() -> some View {
        font(.system(size: 14))
            .foregroundStyle(Color.appTextColor)
    }
}
```

ただ、extension では @State, @Environment などが持てないため、それらを使う場合はカスタム Modifier を使うのが良いです。
まとめると
* @State, @Environment を使うならカスタムの ViewModifier を作成する
* それ以外の場合は extension で済ませる
となります。
