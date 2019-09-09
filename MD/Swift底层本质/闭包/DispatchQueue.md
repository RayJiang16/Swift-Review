## DispatchQueue.async 闭包体内为什么要强制加 self. 访问成员变量？

所有逃逸闭包都需要加 `self.` 访问成员变量，`self` 用于保留/捕获要发送消息的对象的实例。



### Reference

https://stackoverflow.com/questions/53471017/why-escaping-closures-require-us-to-refer-to-self-explicitly
