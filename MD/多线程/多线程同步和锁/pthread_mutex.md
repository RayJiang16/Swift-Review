## pthread_mutex 锁的理解？有哪几种类型？

### pthread_mutex 有哪几种类型？

- [互斥锁](#互斥锁)
- [递归锁](#递归锁)
- [条件锁](#条件锁)



### 互斥锁

```swift
// 初始化锁
var lock = pthread_mutex_t()
// 设置属性
var attr: pthread_mutexattr_t = pthread_mutexattr_t()
pthread_mutexattr_init(&attr)
pthread_mutexattr_settype(&attr, PTHREAD_MUTEX_NORMAL)
pthread_mutex_init(&lock, &attr)
// 销毁锁，用完之后要销毁
pthread_mutex_destroy(&lock)
```

其中锁的类型如下：

```swift
/// 互斥锁，当一个线程加锁后，其余请求锁的线程将形成一个等待队列，并在解锁后按优先级获得锁。这种锁策略保证了资源分配的公平性。
public var PTHREAD_MUTEX_NORMAL: Int32 { get }
/// 检错锁，如果同一个线程请求同一个锁，则抛出一个错误，否则与 PTHREAD_MUTEX_NORMAL 类型动作一致。这样就保证当不允许多次加锁时不会出现最简单情况下的死锁。
public var PTHREAD_MUTEX_ERRORCHECK: Int32 { get }
/// 递归锁，允许同一个线程对同一个锁成功获得多次，并通过多次 unlock 解锁。如果是不同线程请求，则在加锁线程解锁时重新竞争。
public var PTHREAD_MUTEX_RECURSIVE: Int32 { get }
/// PTHREAD_MUTEX_NORMAL
public var PTHREAD_MUTEX_DEFAULT: Int32 { get }
```

```swift
DispatchQueue.global().async {
    self.test(1)
}
self.test(2)

func test(_ n: Int) {
    pthread_mutex_lock(&lock)
    print("Num:\(n) Lock")
    Thread.sleep(forTimeInterval: 2)
    pthread_mutex_unlock(&lock)
    print("Num:\(n) Unlock")
}

// Num:2 Lock
// Num:2 Unlock
// Num:1 Lock
// Num:1 Unlock
```

由于现在是互斥锁，所以在两个不同的线程中使用同一把锁，第二次 lock 的时候会阻塞线程，直到另一个线程 unlock



### 递归锁

```swift
// 初始化锁
var lock = pthread_mutex_t()
// 设置属性
var attr: pthread_mutexattr_t = pthread_mutexattr_t()
pthread_mutexattr_init(&attr)
pthread_mutexattr_settype(&attr, PTHREAD_MUTEX_RECURSIVE)
pthread_mutex_init(&lock, &attr)
// 销毁锁，用完之后要销毁
pthread_mutex_destroy(&lock)
```

```swift
func test(_ n: Int) {
    if n > 3 { return }
    pthread_mutex_lock(&lock)
    print("Num:\(n) Lock")
    test(n+1)
    Thread.sleep(forTimeInterval: 2)
    pthread_mutex_unlock(&lock)
    print("Num:\(n) Unlock")
}

// Num:1 Lock
// Num:2 Lock
// Num:3 Lock
// Num:3 Unlock
// Num:2 Unlock
// Num:1 Unlock
```

递归锁是同一个线程可以多次获得同一个锁，其他线程如果想要获取这把锁，必须要等待，这种锁一般都是用于递归函数的情况。



### 条件锁

```swift
// 创建条件
var cond = pthread_cond_t()
pthread_cond_init(&cond, nil)
```

```swift
/// 删除
@objc func remove() {
    pthread_mutex_lock(&lock)
    
    if array.isEmpty {
        print("Wait")
        // 数据为空就等待（进入休眠，放开锁，被唤醒后，会再次加锁）
        pthread_cond_wait(&cond, &lock)
    }
    
    array.removeFirst()
    print("Remove")
    pthread_mutex_unlock(&lock)
}
/// 添加
@objc func add() {
    pthread_mutex_lock(&lock)
    
    array.append(1)
    print("Add")
    // 激活一个等待该条件的线程
    pthread_cond_signal(&cond)
    // 激活所有等待该条件的线程
    //pthread_cond_broadcast(&_cond)
    
    pthread_mutex_unlock(&lock)
}

// 调用
Thread(target: self, selector: #selector(remove), object: nil).start()
Thread(target: self, selector: #selector(add), object: nil).start()

// Wait
// Add
// Remove
```

上面这段代码，add 和 remove 方法是在两个线程中调用的，先执行 remove 方法，发现没有数据，开始等待；add 方法添加数据后，激活了等待的线程，remove 方法继续执行。



### Reference

https://juejin.im/post/5cf72a42e51d454f71439c8c#heading-13

https://juejin.im/post/5d554410f265da03b21532cd#heading-15