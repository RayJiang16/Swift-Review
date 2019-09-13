## 什么是 Copy on write？

当一个 `struct` 类型的实例被两个变量持有时，这两个变量的指针地址是一样的，当其中一个变量修改 `struct` 中的属性时，Swift 会将这个 `struct` 复制一份，将变量的指针指向新的地址，再进行修改操作。



### Code

```swift
var array1: [Int] = [0, 1, 2, 3] //0x600000078de0
var array2 = array1 //0x600000078de0
array2.append(4)    //0x6000000aa100
```



### Reference

https://www.jianshu.com/p/e8b1336d9d5d