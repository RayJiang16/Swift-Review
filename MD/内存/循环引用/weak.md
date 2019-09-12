## weak 指针实现原理？为什么对象销毁后会被置为 nil？

### weak 指针实现原理？

Runtime 维护了一个 `weak` 表，用于存储指向某个对象的所有 `weak` 指针。`weak` 表其实是一个哈希表，Key 是所指对象的地址，Value 是 `weak` 指针的地址（这个地址的值是所指对象的地址）数组。



### 为什么对象销毁后会被置为 nil？

1. 从 `weak` 表中获取被释放对象的地址为键值的记录
2. 将包含在记录中的所有附有 `weak` 修饰符变量的地址，赋值为 `nil`
3. 将 `weak` 表中该记录删除
4. 从引用计数表中删除废弃对象的地址为键值的记录



### Reference

https://blog.csdn.net/xiaohuoziooo/article/details/88029300