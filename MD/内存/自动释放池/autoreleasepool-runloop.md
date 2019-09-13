## AutoreleasePool 和 Runloop 的关系？

每一个线程，包括主线程，都会拥有一个专属的 `RunLoop` 对象，并且会在有需要的时候自动创建。子线程的`runloop` 需要自己手动创建，如果子线程的 `runloop` 没有任何事件，`runloop`会马上退出。

另外每一个线程都会维护自己的 `autoreleasepool` 堆栈，当 `runloop` 迭代结束时会向 `autoreleasepool` 发送 `release` 消息。



### Reference

https://blog.sunnyxx.com/2014/10/15/behind-autorelease/