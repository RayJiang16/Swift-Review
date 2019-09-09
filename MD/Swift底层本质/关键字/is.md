## is, isKind, isMenber 的区别

### isMember

用来判断该对象是否为指定类的对象



### isKind

用来判断该对象是否为指定类或者指定类的子类的对象



### is

`is` 的作用于 `isKind` 类似，区别在于 `is` 能用于 `struct` 和 `enum`



### Code

```swift
struct A { }
class B: NSObject { }
class C: B { }

let a = A()
let b = B()
let c = C()

// isMember
b.isMember(of: B.self) // true
c.isMember(of: B.self) // false
c.isMember(of: C.self) // true

// isKind
b.isKind(of: B.self) // true
c.isKind(of: B.self) // true

// is
b is B // true
c is B // true
a is A // true
```

