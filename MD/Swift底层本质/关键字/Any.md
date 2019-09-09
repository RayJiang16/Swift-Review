## AnyObject, Any, Anyclass 的区别

### AnyObject

`AnyObject` 可以代表任何 `class` 类型的实例



### Any

`Any` 可以表示任意类型，甚至包括方法 (func) 类型



### Anyclass

通过 `AnyObject.Type` 这种方式得到的就是一个元类型（Meta），也就是 `AnyClass`

```swift
typealias AnyClass = AnyObject.Type
```



### Reference

https://swifter.tips/any-anyobject/

https://www.jianshu.com/p/bab58a90110c
