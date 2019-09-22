## DispatchSourceTimer 和 Timer 比哪个更精准的？

`DispatchSourceTimer` 更精准，因为 `Timer` 会受 `RunLoop` 影响，如果 `RunLoop` 要处理的任务很多，会导致 `Timer` 的精度下降。



### Reference

https://www.jianshu.com/p/faa6ffe4fac3