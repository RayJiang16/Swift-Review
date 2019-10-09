## RunLoop 的监听状态有哪些？怎样监听？

RunLoop 一共有 6 种监听状态：

```swift
let observer = CFRunLoopObserverCreateWithHandler(kCFAllocatorDefault, CFRunLoopActivity.allActivities.rawValue, true, 0) {
(observer, activity) in
    switch activity {
    case .entry:
        print("RunLoop 启动")
    case .beforeTimers:
        print("RunLoop 即将处理 Timer 事件")
    case .beforeSources:
        print("RunLoop 即将处理 Sources 事件")
    case .beforeWaiting:
        print("RunLoop 即将进入休眠")
    case .afterWaiting:
        print("RunLoop 被唤醒")
    case .exit:
        print("RunLoop 退出")
    default:
        break
    }
}
CFRunLoopAddObserver(CFRunLoopGetCurrent(), observer, CFRunLoopMode.defaultMode)
```



### Reference

https://www.cnblogs.com/dashengios/p/10519897.html