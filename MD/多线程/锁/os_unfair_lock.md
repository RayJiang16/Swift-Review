## os_unfair_lock 怎样使用？

`OSSpinLock` 已经不在安全，然后苹果出了 `os_unfair_lock` 来替代 `OSSpinLock`。

```swift
// 初始化锁
var lock = os_unfair_lock()
// 尝试加锁，成功返回 true，失败返回 false
os_unfair_lock_trylock(&lock)
// 加锁
os_unfair_lock_lock(&lock)
// 解锁
os_unfair_lock_unlock(&lock)
```

注意事项：

1. trylock 不会阻塞线程，lock 会阻塞线程。
2. trylock 和 lock 只能选一个使用，如果用了 trylock，在 unlock 之前不能在调用 lock，否则会崩溃。

