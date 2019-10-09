## 你对 Perform Selector 几个方法的理解？哪几种方法是同步执行的？哪几种方法是异步执行的？

1.

```swift
func perform(_ aSelector: Selector!) -> Unmanaged<AnyObject>!
func perform(_ aSelector: Selector!, with object: Any!) -> Unmanaged<AnyObject>!
func perform(_ aSelector: Selector!, with object1: Any!, with object2: Any!) -> Unmanaged<AnyObject>!
```

这三个方法来自 `NSObject`，均为同步执行，主线程和子线程中均可调用成功。等同于直接调用该方法。在需要动态的去调用方法的时候去使用。

2.

```swift
open func perform(_ aSelector: Selector, with anArgument: Any?, afterDelay delay: TimeInterval, inModes modes: [RunLoop.Mode])
open func perform(_ aSelector: Selector, with anArgument: Any?, afterDelay delay: TimeInterval)
```

这两个方法来自 `NSRunLoop`，为异步执行，即使 delay 传参为 0，仍为异步执行。主线程可以直接调用，子线程调用无效，因为这两个方法本质使用 `Timer` 启动的，而子线程的 `RunLoop` 默认是不开启的，不会触发 `Timer`，需要在调用 `perform` 后启动 `RunLoop` 才会生效。
在方法未到执行时间之前，取消方法为：

```swift
open class func cancelPreviousPerformRequests(withTarget aTarget: Any, selector aSelector: Selector, object anArgument: Any?)
open class func cancelPreviousPerformRequests(withTarget aTarget: Any)
```

3.

```swift
open func performSelector(onMainThread aSelector: Selector, with arg: Any?, waitUntilDone wait: Bool, modes array: [String]?)
open func performSelector(onMainThread aSelector: Selector, with arg: Any?, waitUntilDone wait: Bool)
```

这两个方法来自 `NSThread`，在主线程和子线程中均可执行，均会调用主线程的 aSelector 方法；
如果设置 wait 为 true 将阻塞当前线程，等待 `Selector` 执行完之后，才会继续执行后续代码。
如果设置 wait 为 false 则不会阻塞当前线程。

4.

```swift
open func perform(_ aSelector: Selector, on thr: Thread, with arg: Any?, waitUntilDone wait: Bool, modes array: [String]?)
open func perform(_ aSelector: Selector, on thr: Thread, with arg: Any?, waitUntilDone wait: Bool)
```

调用指定线程中的某个方法。分析效果同3。

5.

```swift
open func performSelector(inBackground aSelector: Selector, with arg: Any?)
```

开启子线程在后台运行



### Reference

https://www.jianshu.com/p/fa0933c59c63

https://juejin.im/post/5bee9218e51d4520b7711fc8