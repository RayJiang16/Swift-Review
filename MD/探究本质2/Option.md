## 可选类型的本质？

`Optional` 的本质是一个枚举。“？” 是 Apple 提供的语法糖



#### Code

```swift
public enum Optional<Wrapped> : ExpressibleByNilLiteral {
    case none
    case some(Wrapped)
}
```

