# gradients
https://credo.academy

## code
```swift
import SwiftUI

struct ContentView: View {
  var body: some View {
    VStack {
      // MARK: - 1. BASIC GRADIENT TEXT
      Text("iOS")
        .font(.system(size: 180))
        .fontWeight(.black)
        .foregroundStyle(.teal.gradient)
      
      // MARK: - 2. CUSTOM GRADIENT TEXT
      Text("iOS")
        .font(.system(size: 180))
        .fontWeight(.black)
        .foregroundStyle(
          LinearGradient(
            colors: [.red, .green, .blue],
            startPoint: .topLeading,
            endPoint: .bottomTrailing)
        )
    }
  }
}

struct ContentView_Previews: PreviewProvider {
  static var previews: some View {
    ContentView()
  }
}
```

## result
![gradients](images/gradient.png)
