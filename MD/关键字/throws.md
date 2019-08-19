## throws 和 rethrows 的区别？

#### throws

当一个方法可能会出错，就需要在方法后面加上 `throws`



#### rethrows

当一个闭包作为参数传入到一个方法中，如果这个闭包可能会出错，就需要在方法后面加上 `rethrows`



#### 例子

```swift
enum CustomError: Error {
    case error
}

// throws
func f1(n: Int) throws -> String {
    guard n >= 0 else { throw CustomError.error }
    return String(n)
}

// rethrows
let list = [1, 2, 3]
do {
    try list.map(f1)
} catch {
    // ...
}

// map 的声明
public func map<T>(_ transform: (Element) throws -> T) rethrows -> [T]
```



#### Reference

https://stackoverflow.com/questions/43305051/what-are-the-differences-between-throws-and-rethrows-in-swift
