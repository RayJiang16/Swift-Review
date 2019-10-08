## NSLock 和 NSRecursiveLock 的理解？

### NSLock

`NSLock` 只是在内部封装了一个 `pthread_mutex`，属性为 `PTHREAD_MUTEX_ERRORCHECK`，它会损失一定性能换来错误提示。

`NSLock` 比 `pthread_mutex` 略慢的原因在于它需要经过方法调用，同时由于缓存的存在，多次方法调用不会对性能产生太大的影响。



### NSRecursiveLock

`NSRecursiveLock` 与 `NSLock` 的区别在于内部封装的 `pthread_mutex_t` 对象的类型不同，前者的类型为 `PTHREAD_MUTEX_RECURSIVE`。



### Reference

[pthread_mutex 锁的理解]()

https://juejin.im/post/57f6e9f85bbb50005b126e5f#heading-8