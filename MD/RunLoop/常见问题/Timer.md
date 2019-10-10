## 定时器滑动失效的原因？怎样处理？为什么 Timer 不精准？如何实现精准的定时？

### 定时器滑动失效的原因？

因为 Timer 默认会被加到主线程的 RunLoop 中，mode 为默认，但是 `UIScrollView` 滑动时 RunLoop 的 mode 会从 default 切换到 tracking，这就导致了 Timer 失效。

#### 怎样处理？

在 Timer 加到 RunLoop 时，将 mode 设置为 common。common mode 会将事件分别注册到 default 和 tracking 模式中。



### 为什么 Timer 不精准？

NSTimer 其实就是 CFRunLoopTimerRef，他们之间是 toll-free bridged 的。一个 NSTimer 注册到 RunLoop 后，RunLoop 会为其重复的时间点注册好事件。例如 10:00, 10:10, 10:20 这几个时间点。RunLoop为了节省资源，并不会在非常准确的时间点回调这个Timer。Timer 有个属性叫做 Tolerance (宽容度)，标示了当时间点到后，容许有多少最大误差。

#### 如何实现精准的定时？

使用 GCD 创建定时器。



### Reference

https://blog.ibireme.com/2015/05/18/runloop/