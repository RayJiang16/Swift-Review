## RunLoop 的启动方式有哪些？

RunLoop 有 3 种启动方式

```swift
open func run()
open func run(until limitDate: Date)
open func run(mode: RunLoop.Mode, before limitDate: Date) -> Bool
```



### run()

该方法的作用就是：将接收器置于永久循环中，在此期间处理来自所有附加输入源的数据。其实就是开启 Runloop。

如果没有输入源或定时器连接到运行循环，则此方法立即退出；否则，它通过重复调用 `runMode：beforeDate：` 来在 `NSDefaultRunLoopMode` 中运行接收器。 换句话说，这种方法有效地开始一个无限循环，用于处理来自运行循环的输入源和定时器的数据。

但是不推荐使用，因为这会使线程进入死循环，从而不利于控制 RunLoop。



### run(until limitDate: Date)

该方法的作用就是：运行循环直到指定的日期，在此期间，它处理所有附加的输入源的数据。类同 run 方法，如果没有事件处理也立刻返回；另外增加了 limitDate 避免了无限循环。



### run(mode: RunLoop.Mode, before limitDate: Date) -> Bool

该方法的作用就是：运行循环一次，等待消息处理（好比在PC终端窗口上等待键盘输入）。一旦有合适事件被处理了，则立刻返回；类同 run 方法，如果没有事件处理也立刻返回；有否事件处理由返回 Bool 判断。同样 limitDate 为超时参数。



### Reference

https://www.jianshu.com/p/f4520bdd25c4

https://www.cnblogs.com/shisishao/p/6564997.html