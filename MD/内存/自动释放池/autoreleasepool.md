## 什么是自动释放池？自动释放池的管理原理是怎样的？

### 什么是自动释放池？

`NSAutoreleasePool` 类被用来支持自动引用计数内存管理系统。一个自动释放池存储的对象当自己被销毁的时会向其中的对象发送 release 消息。



### 自动释放池的管理原理是怎样的？

在一个自动引用计数的环境中（并不是垃圾回收机制），一个包含了多个对象的 NSAutoreleasePool 对象能够接收 autorelease 消息并且当销毁它的时候会对每一个池子中的对象发送 release 消息。因此，发送 autorelease 而不是 release 消息延长了对象的生命周期直到 pool 被清空的时候（当对象被保留的时候会更久）。一个对象能够被放到同一个池子中许多次，在这种情况下每放一次都会收到一个 release 消息。



### Reference 

https://www.jianshu.com/p/554c9fe0f041