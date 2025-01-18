# learning-swift

learning through Udemy  
★SwiftUI Masterclass 2025 – iOS App Development & SwiftData★


## SF Symbol : vector graphic supported only apple platform

※ 주의 할 약관사항 : 
Apple platform에서만 사용할 것  
수정, 재생산, 배포 금지  
로고 등으로 사용 금지  
apple이 제한 사항을 위반해 사용된  symbol에 대해 사용 중단 요구시 신속히 응할 것


## Swift UI Link

source : https://developer.apple.com/documentation/swiftui/link  
available up to 10s 14.0


```swift
struct Link<Label> where Label : View
```

## Examples : 
<!-- image -->
```swift
Link("Go to Apple:, destination:
  URL(string: https://apple.com")!)
```
<!-- image -->
```swift
Link("Call to Action",
destination: URL(string : "tel:1234567890")!)
```
<!-- image -->
```swift
Link("Send an Email",
  destination: URL(string : "cksgnl0523@gmail.com")!)
```

