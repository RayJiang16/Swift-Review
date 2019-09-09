## .type 和 type(of: ) 的区别

### .type

```swift
let staicMetaType: String.Type = String.self
```



### type(of: )

```swift
let instanceMetaType: String.Type = type(of: "string")
```



### 区别

他们都用于获得元类型的值，`.self` 取到的是静态的元类型，声明的时候是什么类型就是什么类型。`type(of:)` 取的是运行时候的元类型，也就是这个实例的类型。



### Reference

https://www.jianshu.com/p/36083d0404b9
