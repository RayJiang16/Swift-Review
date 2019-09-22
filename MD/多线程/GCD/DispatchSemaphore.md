## DispatchSemaphore 的理解？对信号量控制方法的理解？信号量底层原理是怎样？

### DispatchSemaphore 的理解？

`DispatchSemaphore`，通常称作信号量，顾名思义，它可以通过计数来标识一个信号，这个信号怎么用呢，取决于任务的性质。通常用于对同一个资源访问的任务数进行限制。

例如，控制同一时间写文件的任务数量、控制端口访问数量、控制下载任务数量等。



### 信号量底层原理是怎样？

详情请看这篇[文章](https://juejin.im/post/5c761d36f265da2d84109277)。



### Reference

https://juejin.im/post/5acaea17f265da239a601a01#heading-41

https://juejin.im/post/5c761d36f265da2d84109277