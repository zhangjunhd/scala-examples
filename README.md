# 快学Scala
![cover](https://img1.doubanio.com/lpic/s22713467.jpg)

[豆瓣链接](https://book.douban.com/subject/19971952/)

    作者: [美] C. S. 霍斯曼
    出版社: 电子工业出版社
    原作名: Scala for the Impatient
    译者: 高宇翔
    出版年: 2012-10
    页数: 408
    定价: 79.00元
    装帧: 平装
    ISBN: 9787121185670

## Scala笔记索引

* [Scala笔记1-基本类型](scala-note1-data-type.md)
  * Scala基本类型
  * Scala BigDecimal
  * 乘方，素数，随机数(`Random`)
  * Scala date/time
  * Scala String(`format`, `mkString`,`mkString`, `stripLineEnd`, `==`, `count`, `split`, `foreach(println)`, `distinct`, `diff`, `intersect`, `take`, `drop`, `takeRight`, `dropRight`, `substring`)
  * 类型检查与转换(`isInstanceOf`, `asInstanceOf`, `classOf`)
  * 类反射
* [Scala笔记2-控制结构与函数](scala-note2-condition-and-function.md)
  * `for`
  * `yeild`
  * 加入guard
  * 变长参数
  * 递归
* [Scala笔记3-数组](scala-note3-array.md)
  * `Array`
  * `ArrayBuffer`
  * 数组遍历
  * 常用算法(`sum`,`min`,`max`,`count`,`sort`)
  * 多维数组
  * 与Java互操作(`JavaConversions.bufferAsJavaList`)
* [Scala笔记4-映射与元组](scala-note4-map-and-tuple.md)
  * map声明，赋值，追加，减少
  * map迭代
  * 加入guard
  * 使用map实现wordcount
  * 使用hashmap统计词频
  * 与Java互操作`JavaConversions.mapAsScalaMap`
  * 元组`zip`,`partition`
* [Scala笔记5-类](scala-note5-class.md)
  * getter/setter
  * 对象私有字段`private[this]`
  * `BeanProperty`
  * 主构造和辅助构造器
  * 伴生对象(companion object)
  * 嵌套类(类型投影(type projection),外部类的this引用)
  * apply
  * 重写字段
  * 结构类型
  * 懒值lazy
  * 构造顺序与提前定义
  * 对象相等性(equals)
* [Scala笔记6-枚举](scala-note6-enumeration.md)
  * `Enumeration`
  * 类型别名
* [Scala笔记7-文件操作](scala-note7-file.md)
  * 读写文件
  * 缓存读
  * 遍历目录
  * 序列化
* [Scala笔记8-进程控制](scala-note8-process.md)
  * `ProcessBuilder`
* [Scala笔记9-正则表达式与文法解析](scala-note9-regex.md)
  * 正则表达式(`Regex`)
  * 正则表达式组
  组合解析器操作(`RegexParsers`)
* [Scala笔记10-特质](scala-note10-trait.md)
  * 自身类型(`this: type`)
  * 结构类型(structural type)
* [Scala笔记11-apply函数](scala-note11-apply.md)
  * `apply`
  * `unapply`
  * `update`
  * `unapplySeq`
* [Scala笔记12-高阶函数](scala-note12-high-order-function.md)
  * 闭包
  * SAM(single abstract method)
  * 柯里化(Currying)
  * 控制抽象
* [scala笔记13-集合](scala-note13-collections.md)
  * 将函数映射到集合(`map`,`flatMap`, `collect`)
  化简折叠和扫描(`reduceLeft`,`reduceRight`, `foldLeft`, `foldRight`, `scanLeft`, `scanRight`)
  * 拉链操作(`zip`, `zipWithIndex`)
  * 迭代器
  * 流
  * 懒视图(`view`)
  * 与Java集合的互操作
  * 线程安全的集合
  * 并行集合
* [scala笔记14-模式匹配与样例类](scala-note14-pattern-match.md)
  * 类型模式(match)
  * 提取器
  * 样例类(`copy`)
  * Option类型(`Option`,`Some`,`None`, `Either`, `Left`, `Right`)
  * 偏函数
* [scala笔记15-注解](scala-note15-annotations.md)
* [scala笔记16-xml](scala-note16-xml.md)
* [scala Json](http://www.furida.mu/blog/2012/09/18/beautiful-json-parsing-in-scala/)
* [scala笔记17-类型参数与隐式转换](scala-note17-type-parameters.md)
  * 类型变量界定
  * 视图界定
  * 上下文界定
  * 多重界定
  * 约束类型
  * 协变
  * 对象不能泛型
  * 类型通配符
  * 隐式转换
  * 隐式参数
* [scala笔记18-高级类型](scala-note18-advanced-types.md)
  * 单例类型(`this.type`)
  * 结构类型
  * 存在类型
  * 蛋糕模式
  * 抽象类型(abstract type)
  * 家族多态
  * 高等类型
