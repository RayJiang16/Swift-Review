## GCD 和 Runloop 的关系？

实际上 RunLoop 底层也会用到 GCD 的东西，比如 RunLoop 的超时时间就是使用 GCD 中的 `dispatch_source_t`来实现的。

但同时 GCD 提供的某些接口也用到了 RunLoop， 例如 `dispatch_async()`。当调用 `dispatch_async(dispatch_get_main_queue(), block)` 时，libDispatch 会向主线程的 RunLoop 发送消息，RunLoop会被唤醒，并从消息中取得这个 block，并在回调 `__CFRUNLOOP_IS_SERVICING_THE_MAIN_DISPATCH_QUEUE__()` 里执行这个 block。但这个逻辑仅限于 dispatch 到主线程，dispatch 到其他线程仍然是由 libDispatch 处理的。



### Reference

https://blog.ibireme.com/2015/05/18/runloop/

https://blog.csdn.net/u011619283/article/details/53783650