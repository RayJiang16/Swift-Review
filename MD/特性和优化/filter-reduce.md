## filter, reduce 的区别？

#### filter

用于筛选，参数是一个用来判断是否筛除的筛选闭包，根据闭包函数返回的 Bool 值来过滤值。为 true 则加入到结果数组中。



#### reduce

给定一个类型为U的初始值，把数组[T]中每一个元素传入到combine的闭包函数里面，通过计算得到最终类型为U的结果值。



#### Code

```swift
let list = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10].filter{ $0 % 2 == 0 }
// list = [2, 4, 6, 8, 10]

let sum = [1, 2, 3, 4].reduce(into: 0) { (result, num) in
    result += num
}
// sum = 10
```

