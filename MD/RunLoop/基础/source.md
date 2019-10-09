## RunLoop 的事件源有哪些？特点是什么？

Run Loop Source 分为 Source、Observer、Timer 三种，他们统称为 ModeItem。



### CFRunLoopSource

根据官方的描述，CFRunLoopSource 是对 input sources 的抽象。CFRunLoopSource 分 source 0 和source 1。

#### source 0 

是 App 内部事件，由 App 自己管理的 UIEvent、CFSocket 都是 source 0。

#### source 1 

由 RunLoop 和内核管理，可以监听系统端口和通过内核和其他线程通信，接收、分发系统事件，它能够主动唤醒 RunLoop (由操作系统内核进行管理，例如 CFMessagePort 消息)。



### CFRunLoopObserver

CFRunLoopObserver 是观察者，可以观察RunLoop的各种状态，并抛出回调。

CFRunLoopObserver 可以观察的状态有如下 6 种:

```swift
public static var entry: CFRunLoopActivity { get } // 即将进入 run loop
public static var beforeTimers: CFRunLoopActivity { get } // 即将处理 timer
public static var beforeSources: CFRunLoopActivity { get } // 即将处理 source
public static var beforeWaiting: CFRunLoopActivity { get } // 即将进入休眠
public static var afterWaiting: CFRunLoopActivity { get } // 被唤醒但是还没开始处理事件
public static var exit: CFRunLoopActivity { get } // run loop 已经退出
public static var allActivities: CFRunLoopActivity { get }
```

Runloop 通过监控 Source 来决定有没有任务要做，除此之外，我们还可以用 Runloop Observer 来监控 Runloop 本身的状态。 Runloop Observer 可以监控上面的 Runloop 事件。



### CFRunLoopTimer

CFRunLoopTimer 是定时器，具有以下特点：

- CFRunLoopTimer 是定时器，可以在设定的时间点抛出回调。
- CFRunLoopTimer 和 NSTimer 是 toll-free bridged 的，可以相互转换。





### Reference

https://juejin.im/post/5aca2b0a6fb9a028d700e1f8#heading-4