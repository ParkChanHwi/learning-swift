# Title: AsyncImage(비동기 이미지)

SwiftUI의 `AsyncImage`는 원격 이미지를 비동기적으로 로드하고 표시하는 기능을 제공합니다.  
이 문서에서는 `AsyncImage`의 다양한 기능을 구현한 코드를 설명합니다.

---

## 기본 설정

- **이미지 크기 조정:** `scale` 매개변수를 사용하여 이미지의 크기를 변경할 수 있습니다.
- **Modifier 사용:** 이미지에 `Modifier`를 적용하여 커스터마이징할 수 있습니다.
- **플레이스홀더:** 이미지를 로드하거나 오류가 발생했을 때 표시할 플레이스홀더를 설정할 수 있습니다.
- **애니메이션:** 로드된 이미지를 애니메이션과 함께 표시할 수 있습니다.



## 코드

### 1. Basic: 원격 이미지 로드
다음 코드는 `AsyncImage`를 사용하여 원격 이미지를 단순히 로드하는 기본적인 방법을 보여줍니다.

```swift
// MARK: - 1. BASIC
AsyncImage(url: URL(string: imageURL))
```

### 2. Scale: 이미지 크기 조정
scale 매개변수를 사용하여 원격 이미지를 로드할 때 크기를 조정할 수 있습니다.
아래 코드에서는 이미지 스케일을 3.0으로 설정합니다.

```swift
// MARK: - 2. SCALE
AsyncImage(url: URL(string: imageURL), scale: 3.0)
```

### 3. Placeholder: 플레이스홀더 설정
이미지를 로드하는 동안 또는 오류가 발생했을 때 보여줄 플레이스홀더를 설정할 수 있습니다.
여기서는 photo.circle.fill 아이콘을 플레이스홀더로 사용합니다.

```swift
// MARK: - 3. PLACEHOLDER
AsyncImage(url: URL(string: imageURL)) { image in
    image.imageModifier()
} placeholder: {
    Image(systemName: "photo.circle.fill").iconModifier()
}
.padding(40)
```
### 4. Phase: 상태별 이미지 처리  
AsyncImage의 phase 매개변수를 사용하여 로드 상태에 따라 이미지를 처리합니다.
	•	success: 이미지가 성공적으로 로드되었을 때
	•	failure: 이미지 로드 실패 시
	•	empty: 아직 로드되지 않았을 때
 
```swift
 // MARK: - 4. PHASE
AsyncImage(url: URL(string: imageURL)) { phase in
    switch phase {
    case .success(let image):
        image.imageModifier()
    case .failure(_):
        Image(systemName: "ant.circle.fill").iconModifier()
    case .empty:
        Image(systemName: "photo.circle.fill").iconModifier()
    @unknown default:
        ProgressView()
    }
}
.padding(40)
```

### 5. Animation : 애니메이션 추가
이미지가 로드된 후 애니메이션을 사용해 자연스럽게 표시할 수 있습니다.
아래 코드에서는 .spring 애니메이션을 적용하고 transition(.scale)을 추가했습니다.

```swift
// MARK: - 5. ANIMATION
AsyncImage(
    url: URL(string: imageURL), 
    transaction: Transaction(animation: .spring(response: 0.5, dampingFraction: 0.6, blendDuration: 0.25))
) { phase in
    switch phase {
    case .success(let image):
        image
            .imageModifier()
            .transition(.scale)
    case .failure(_):
        Image(systemName: "ant.circle.fill").iconModifier()
    case .empty:
        Image(systemName: "photo.circle.fill").iconModifier()
    @unknown default:
        ProgressView()
    }
}
.padding(40)
```

### Extension: Image Modifier
이미지의 스타일을 커스터마이징하기 위해 Image를 확장했습니다.
imageModifier는 이미지를 resizable 및 scaledToFit으로 설정하며,
iconModifier는 이를 확장하여 아이콘 스타일을 추가합니다.

```swift
extension Image {
    func imageModifier() -> some View {
        self
            .resizable()
            .scaledToFit()
    }
    
    func iconModifier() -> some View {
        self
            .imageModifier()
            .frame(maxWidth: 128)
            .foregroundColor(.purple)
            .opacity(0.5)
    }
}
```

### KeyPoint
	1.	AsyncImage는 비동기적으로 이미지를 로드하며 다양한 상태를 처리할 수 있습니다.
	2.	플레이스홀더와 애니메이션을 추가하여 사용자 경험을 향상시킬 수 있습니다.
	3.	Modifier를 사용해 재사용 가능한 스타일을 정의하고, 코드를 간결하게 작성할 수 있습니다

### source
credo ios lecture
