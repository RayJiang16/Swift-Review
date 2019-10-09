## RunLoop 的退出方式有哪些？

在 [RunLoop 的启动方式有哪些？](run.md)这篇文章里说到了 3 种启动的方式，其中第一个启动方式是会一直循环下去的，其他 2 个启动方式都有超时时间的，过了超时时间就退出了。

另外系统提供了 `CFRunLoopStop()` 来结束 RunLoop，**但是** `CFRunLoopStop()` 方法只会结束当前的 `runMode:beforeDate:` 调用，而不会结束后续的调用。

所以想要控制 RunLoop 的退出时机有两个方案：

1 使用 `CFRunLoopRun()` 启动 RunLoop

2

```swift
BOOL shouldKeepRunning = YES; // global
NSRunLoop *theRL = [NSRunLoop currentRunLoop];
while (shouldKeepRunning && [theRL runMode:NSDefaultRunLoopMode beforeDate:[NSDate distantFuture]]);
```



### Reference

https://juejin.im/post/579583ba6be3ff006613628c
