## map, flatMap, compactMap 的区别？

#### map

可以对数组中的每一个元素做一次处理



#### flatMap

能把数组中存有数组的数组（二维数组、N维数组）展平变成一个新的数组



#### compactMap

能把数组中的 nil 过滤掉，返回一个新的数组



#### Code

```swift
let m1 = [1, 2, 3, 4, 5].map{ $0 * 2 } // [2, 4, 6, 8, 10]
let m2 = [[1, 2], [3, 4]].flatMap{ $0 } // [1, 2, 3, 4]
let m3 = [1, 2, 3, nil, 5, 6].compactMap{ $0 } // [1, 2, 3, 5, 6]
```

