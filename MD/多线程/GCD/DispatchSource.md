## DispatchSource 的理解？

GCD 中提供了一个 `DispatchSource` 类，它可以帮你监听系统底层一些对象的活动，例如这些对象： `Mach port`、`Unix descriptor`、`Unix signal`、`VFS node`，并允许你在这些活动发生时，向队列提交一个任务以进行异步处理。




### Reference

https://juejin.im/post/5acaea17f265da239a601a01#heading-29