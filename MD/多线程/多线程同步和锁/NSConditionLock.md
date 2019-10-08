## NSConditionLock 条件锁的理解？怎样使用？

### NSConditionLock 条件锁的理解？

`NSConditionLock` 是借助 `NSCondition` 来实现的，而 `NSCondition `的底层是通过条件变量(condition variable) `pthread_cond_t` 来实现的。条件变量有点像信号量，提供了线程阻塞与信号机制，因此可以用来阻塞某个线程，并等待某个数据就绪，随后唤醒线程。



### Code

```swift
let lock = NSConditionLock(condition: 0)
DispatchQueue.global().async {
    self.lock.lock(whenCondition: 0)
    print(1)
    self.lock.unlock(withCondition: 10)
}
DispatchQueue.global().async {
    self.lock.lock(whenCondition: 5)
    print(2)
    self.lock.unlock()
}
DispatchQueue.global().async {
    self.lock.lock(whenCondition: 10)
    print(3)
    self.lock.unlock(withCondition: 5)
}

// 1
// 3
// 2
```

1. 初始化 NSConditionLock 对象时，设置了加锁条件为 0
2. 执行第一段的时候，传入的条件是 0，所以加锁成功，解锁时将条件设为 10
3. 执行第二段的时候，传入的条件是 5，不符合当前条件，线程开始等待
4. 执行第三段的时候，传入的条件是 10，符合当前条件，加锁成功，解锁是将条件设为 5
5. 第二段线程被唤醒，继续执行



### Reference

https://juejin.im/post/57f6e9f85bbb50005b126e5f#heading-14