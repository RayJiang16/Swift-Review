## .self 的理解

#### 元类型

元类型就是类型的类型。

比如我们说 5 是 `Int` 类型，此时 5 是 `Int` 类型的一个值。但是如果我问 `Int` 类型占用多少内存空间，这个时候与具体某个值无关，而和类型的信息相关。如果要写一个函数，返回一个类型的实例内存空间大小。那么这个时候的参数是一个类型数据，这个类型数据可以是直接说明的比如是 `Int` 类型，也可以从一个值身上取，比如 5 这个值的类型。这里的类型数据，就是一个类型的类型，术语表述为元类型：metaType。



#### .Type 与 .self

Swift 中的元类型用 `.Type` 表示。比如 `Int.Type` 就是 `Int` 的元类型。
类型与值有着不同的形式，就像 `Int` 与 5 的关系。元类型也是类似，`.Type` 是类型，类型的 `.self` 是元类型的值。

```swift
let intMetatype: Int.Type = Int.self
```



#### Code

```swift
// TableView 注册 Cell 的声明
open func register(_ cellClass: AnyClass?, forCellReuseIdentifier identifier: String)
// 调用
tableView.register(UITableViewCell.self, forCellReuseIdentifier: "cell")
```



#### Reference

https://www.jianshu.com/p/36083d0404b9