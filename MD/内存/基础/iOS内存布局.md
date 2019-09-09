## iOS 内存布局结构？

![](https://github.com/RayJiang16/Swift-Review/blob/master/Image/内存/ios-memory-layout.png)

- 代码段：编译之后的代码
- 数据段：
  - 字符串常量：比如NSString *str = @"123"
  - 已初始化数据：已初始化的全局变量、静态变量等
  - 未初始化数据：未初始化的全局变量、静态变量等
- 堆：函数调用开销，比如局部变量。分配的内存空间地址越来越小
- 栈：通过 alloc、malloc、calloc 等动态分配的空间，分配的内存空间地址越来越大



#### Reference

https://www.jianshu.com/p/5fadc22ba33b