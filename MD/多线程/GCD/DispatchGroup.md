## DispatchGroup 的底层原理是什么？一般用在什么场景？有哪几种添加进组的方式？

### DispatchGroup 的底层原理是什么？

`DispatchGroup` 是基于 `DispatchSemaphore` 实现的，详情请看这篇[文章](https://www.jianshu.com/p/e93fd15d93d3)。



### 一般用在什么场景？

一般用于一个任务依赖于多个耗时任务时使用，比如页面需要等待两个（及以上）接口返回后再刷新的情况。



### 有哪几种添加进组的方式？

有两种进组方式。

```swift
let group = DispatchGroup()
let queue = DispatchQueue.global()

// 第一种方式
queue.async(group: group) {
    print("1")
}

// 第二种方式，enter 和 leave 需要成对出现
group.enter()
queue.sync {
    print("2")
    group.leave()
}
```



### Reference

https://www.jianshu.com/p/e93fd15d93d3

https://juejin.im/post/5acaea17f265da239a601a01#heading-24