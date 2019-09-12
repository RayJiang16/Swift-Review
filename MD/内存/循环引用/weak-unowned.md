## weak 和 unowned 有什么区别？

为了避免循环引用，需要用弱引用来代替强引用。

`weak` 和 `unowned` 都是弱引用，他们的区别是

`weak` 标识的变量，当引用的对象被释放会将指针指向 `nil`，所以 `weak` 的变量一定是可选型。

`unowned` 标识的变量，当引用的对象被释放，它仍然会指向被释放的内存区域，如果这个时候访问对象会导致程序崩溃。

关于两者使用的选择，Apple 给我们的建议是如果能够确定在访问时不会已被释放的话，尽量使用 `unowned` ，如果存在被释放的可能，那就选择用 `weak`。



### Reference

https://www.cnblogs.com/yajunLi/p/5972176.html