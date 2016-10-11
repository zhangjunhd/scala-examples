## Scala笔记12-高阶函数
### 作为值的函数

```scala
import scala.math._

val fun = ceil _   // _将ceil方法转成了函数
```

从技术上讲，_将ceil方法转成了函数。ceil函数后的_意味着你确实指的是这个函数，而不是碰巧忘记了给它送参数。

fun的类型是(Double)=>Double，意为接受Double参数并返回Double的函数。能够对fun做的有：调用，传递。

```scala
val num = 3.14

fun(num)  // 返回4.0，调用fun

Array(3.14, 1.42, 2.0).map(fun)  //返回Array(4.0, 2.0, 2.0)，将fun作为变量传递
```

### 匿名函数

```scala
(x: Double) => 3 * x  // 该匿名函数将传给它的参数乘3
```

### 带函数参数的函数

```scala
def valueAtOneQuarter(f: (Double) => Double) = f(0.25)

valueAtOneQuarter(ceil _) // 1.0
valueAtOneQuarter(sqrt _) // 0.5 (0.5 * 0.5 = 0.25)
```

该函数的类型是： ((Double) => Double) => Double。

还有可以返回一个函数的函数：

```scala
def mulBy(factor: Double) = (x: Double) => factor * x

// mulBy可以产出任何两个数相乘的函数
val quintuple = mulBy(5)  // (x: Double) => 5 * x
quintuple(20)  // 5 * 20
```

这样接受函数参数，或者是返回函数的函数，被称为`高阶函数`（higher-order function）。

### 参数（类型）推断

前面有定义高阶函数 def valueAtOneQuarter(f: (Double) => Double) = f(0.25)，因为已知参数的类型，所以Scala会尽可能推断出类型，在传入参数时，可以省掉一些内容。

```scala
valueAtOneQuarter((x: Double) => 3 * x)  // 完整写法
valueAtOneQuarter((x) => 3 * x)  // 已知参数类型，可以省掉Double
valueAtOneQuarter(x => 3 * x)  // 只有一个参数时，可以省去()
valueAtOneQuarter(3 * _)  // 参数只在右侧出现一次，可以用_替换
```

注意，这些简写方式仅在参数类型已知的情况下有效。

```scala
val fun = 3 * _ // 错误：无法推断类型
val fun = 3 * (_: Double) // OK
val fun:(Double) => Double = 3 * _ // OK
```

### 闭包
`闭包`(closure)由代码和代码用到的任何非局部变量定义构成。

```scala
def mulBy(factor: Double) = (x: Double) => factor * x

val triple = mulBy(3)
val half = mulBy(0.5)
```

这些函数实际上是以类的对象方式实现的，该类有一个实例变量factor和一个包含了函数体的apply方法。

### SAM转换

在Scala中，要某个函数做某件事时，会传一个函数参数给它。而在Java中，并不支持传送参数。通常Java的实现方式是将动作放在一个实现某接口的类中，然后将该类的一个实例传递给另一个方法。很多时候，这些接口只有单个抽象方法（single abstract method），在Java中被称为`SAM类型`。

```scala
var counter = 0

val button = new JButton("Increment")
button.addActionListener(new ActionListener {
  override def actionPerformed(event: ActionEvent) {
    count += 1
  }
})
```

给addActionListener传一个函数参数:

```scala
button.addActionListener((event: ActionEvent) => counter += 1)
```

为了使这个语法真的生效，需要提供一个`隐式转换`:

```scala
implicit def makeAction(action: (ActionEvent) => Unit) =
  new ActionListener {
    override def actionPerformed(event: ActionEvent) { action(event) }
  }
```

### 柯里化(Currying)

`柯里化`指的是将原来接受两个参数的函数变成新的接受一个参数的函数的过程。新的函数返回一个以原有第二个参数作为参数的函数。

```scala
def mulOneAtATime(x: Int) = (y: Int) => x * y

// 计算两个数的乘积
mulOneAtATime(6)(7)

// 多参数的写法
def mul(x: Int, y: Int) = x * y
```

mulOneAtATime(6)返回的是函数(y: Int)=>6*y，再将这个函数应用到7，最终得到结果。柯里化函数可以在Scala中简写：

```scala
def mulOneAtATime(x: Int)(y: Int) = x * y
```

可以利用柯里化把某个函数参数单独拎出来，提供更多用于类型推断的信息。

```scala
val a = Array("Hello", "World")
val b = Array("hello", "world")
a.corresponds(b)(_.equalsIgnoreCase(_))
```

corresponds的类型声明如下：

```scala
def corresponds[B](that: GenSeq[B])(p: (T, B) ⇒ Boolean): Boolean
```

方法有两个参数，that序列和p函数，其中p函数有两个参数，第二个参数类型是与that序列一致的。因为使用了柯里化，我们可以省去第二个参数中B的类型，因为从that序列中推断出B的类型。于是，_equalsIgnoreCase(_)这个简写就符合参数的要求了。

### 控制抽象

Scala中，可以将一系列语句归组成不带参数也没有返回值的函数。

```scala
def runInThread(block: () => Unit) {
  new Thread {
    override def run() { block() }
  }.start()
}

// 调用
runInThread { () => println("Hi"); Thread.sleep(10000); println("Bye") }
```

可以去掉调用中的()=>，在参数声明和调用该函数参数的地方略去()，保留=>。

```scala
def runInThread(block: => Unit) {
  new Thread {
    override def run () { block }
  }.start()
}

// 调用
runInThread { println("Hi"); Thread.sleep(10000); println("Bye") }
```

Scala程序员可以构建控制抽象：看上去像是编程语言关键字的函数。

```scala
def until(condition: => Boolean)(block: => Unit) {
  if (!condition) {
    block
    until(condition)(block)
  }
}

// 使用
var x = 10
until (x == 0) {
  x -= 1
  println(x)
}
```

这样的函数参数专业术语叫做`换名调用参数`（常规的参数叫换值调用参数）。函数在调用时，换名调用参数的表达式不会被求值，表达式会被当做参数传递下去。
