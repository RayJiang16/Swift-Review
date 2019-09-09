## 大概描述一下 Swift 的编译流程？Swift 和 OC 的区别？

### 大概描述一下 Swift 的编译流程？

![](https://github.com/RayJiang16/Swift-Review/blob/master/Image/Swift底层本质/swift-compilation-process.jpg)

1. Swift 代码转换成 **ATS**（抽象语法树）
2. ATS 转换成 **SIL** （Swift 中间语言）
3. 由原始 SIL 转换成 标准的 SIL
4. SIL 转换成 **LLVM IR** （底层虚拟机的中间表示层）
5. LLVM 转换成 **Assembly** （汇编）
6. Assembly 转换成 **Executable** （可执行文件）



### Swift 和 OC 的区别？

未知



### Reference

https://github.com/apple/swift/blob/master/docs/CompilerPerformance.md
