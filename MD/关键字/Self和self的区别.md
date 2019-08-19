## Self 和 self 的区别

#### self

`self` 在实例方法中代指当前实例，在类方法中则代指当前类。



#### Self

`Self` 有两种不同的用途

1. 在 `Protocol` 中用于限制相关的类型
2. 在 `Class/static` 方法中充当方法的返回值类型



#### 例子

```swift
extension BinaryInteger {
    func squared() -> Self { // Self 用于限制类型
        return self * self // self 获取当前实例
    }
}
```



#### Reference

https://forums.developer.apple.com/thread/5479