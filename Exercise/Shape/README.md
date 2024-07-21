# Shape

## Overview

In SwiftUI, there is a protocol called `Shape`
`Shape` represents shapes such as circles, squares and more.

```swift
struct ContentView: View {
    var body: some View {
        VStack {
            Circle()
                .stroke(.orange, lineWidth: 3)
            Rectangle()
                .foregroundStyle(.brown)
            Capsule()
                .fill(.cyan)
        }
        .foregroundStyle(.red)
        .frame(width: 200, height: 300)
    }
}
```

<img width="189" alt="Screenshot 2024-07-20 at 9 28 28 PM" src="https://github.com/user-attachments/assets/609a528f-8a68-4b4d-aea5-669902df5293">

It is used to customize the shape of a `View` by cutting out the shape or applying it to other `View`.

```swift
struct ContentView: View {
    var body: some View {
        Text("Text")
            .frame(minWidth: 128)
            .padding(.vertical, 8)
            .background(.cyan)
            .font(.title.bold())
            .clipShape(Capsule())
            .foregroundStyle(.white)
    }
}
```

<img width="137" alt="Screenshot 2024-07-20 at 11 04 42 PM" src="https://github.com/user-attachments/assets/f7c0d14c-6b0e-4cde-bf1f-c0b91386feb5">

Shape represents only the shape itself, so you always need to specify its position and size. By default, when yu place a Shape directly as a View, it will expand to fill its parent View.

# カスタムのShape

It is also possible to define custom Shape

```swift
struct Diamond: Shape {
    func path(in rect: CGRect) -> Path {
        Path { path in
            path.move(to: .init(x: rect.midX, y: 0))
            path.addLine(to: .init(x: rect.maxX, y: rect.midY))
            path.addLine(to: .init(x: rect.midX, y: rect.maxY))
            path.addLine(to: .init(x: rect.minX, y: rect.midY))
        }
    }
}
```
<img width="291" alt="Screenshot 2024-07-21 at 6 25 09 PM" src="https://github.com/user-attachments/assets/336ec25c-fa66-4ec4-a5ba-f3158e171904">

# Shapeの合成

It is possible to combine shpae in SwiftUI by overlaying them or cutting one shape out of another.

```swift
struct ContentView: View {
    var body: some View {
        Circle()
            .overlay(
                Diamond()
                    .fill(Color.white)
            )
            .frame(width: 120)
    }
}
```
<img width="131" alt="Screenshot 2024-07-21 at 6 48 02 PM" src="https://github.com/user-attachments/assets/05ad231a-7a8f-4c02-a659-a5c737188f19">
