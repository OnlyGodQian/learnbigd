# Scala类与对象，类型与操作

## 类的声明

```scala
class MyClass{
    
    private var num = 0 // 如果想要不对外开放，使用private，如果不写，默认就是public
    
    //方法
    //花括号前没有=号，这种情况下，返回值类型一定是Unit，也就是空,所以如果想有返回值，一定要加=号
    def add(b:Byte){
        num += b
    }
    //如果计算表达式只有一行，可以省略掉花括号
    def add1(b:Byte):Unit = num += b
    
    //有返回值的正常方法：
    def checkSum(): Int = ~(num & OxFF) + 1
}
```

##Singleton对象

普通类中不能定义静态成员，要定义静态成员，就定义在一个单例类中

```scala
//定义位置：如果与普通类的名字一样，那么成为普通类的伴生对象，要定义在同一个源文件中
//类和伴生对象可以互相访问其私有成员
object MyClass{
    
    //类中的成员和普通类一样
    def calculate(s:String):Int = {
        //TODO...
    }
}

//类似于java中的静态方法工具类
//使用方式也是类名点方法名
MyClass.calculate("a")
```

## Scala程序运行

### 需要一个main函数

```scala
//在单例对象中定义main函数
object Summer{
    def main(args:Array[String]){
    //TODO..
	}  
}
```

### 需要编译执行

```
编译：
scalac MyClass.scala Summer.scala 
执行：
scala Summer of love
```



## Application特质

让单例对象继承Application，然后把要写在main函数里面的函数体，直接写在花括号中，不用写main了，因为Application已经提供了

```scala
object Summer extends Application{
    
    //TODO..
    for(season <- List("fall","winter","spring"))
    	println(season)
    
}
```

## 基本类型

包括String和值类型。

值类型包括：

* Byte
* Short
* Int
* Long
* Char
* String
* Float
* Double
* Boolean

String 在java.lang包下

其他值类型在scala包下

**可以直接用字面量，也就是，直接使用具体的值，而不需要使用引用。**

### 符号字面量

```scala
//语法： 'symbol
val a = 'hello
a: Symbol = 'hello
//例如方法：
def updateRecordByName(r:Symbol,value Any){
    //TODO..
}
```

## 操作符和方法

+-*/ 这些符号其实都是方法名。

以上的几个是**中缀**操作符

```scala
//例如：
val a = 3 + 5 // +号是中缀操作符，实际上是 3.+（5）
val b = "hello"
val c = b indexOf 'o'//这个indexOf也是中缀操作符，实际上是 b.indexOf('o')
```

任何方法都可以是操作符

除了中缀操作符，还有前缀和后缀操作符

```scala
//前缀操作符只有 + - ！ ~ 四种
val a = -3.0 //前缀操作符，实际上Scala调用了(3.0).unary_-  ,就是给操作符加上“unary_”的前缀
//如果给类定义了 unary_*方法，也不能使用*p

//后缀操作符，就是不用点和括号调用的不带参数的方法，比如：
val s = "Hello"
val s1 = s toLowerCase//toLowerCase就成了后缀操作符了
```

###数学运算和关系运算和位运算

与java类似

### 相等性判断

直接使用 == 或者 !=

因为 == 已经被仔细加工过了，在大多数情况下都可以实现合适的相等性比较

```scala
//比较规则是：首先检查左侧是否为null，如果不是，调用左操作数的equals方法。而精确的比较取决于做操作数的equals方法定义。由于有了自动的null检查，因此不需要手动再检查一遍了。
scala> 1 == 1.0
res3: Boolean = true

scala> List(1,2,3) == null
res4: Boolean = false
```

## 基本类型有对应的富包装类

富包装类提供了更多的操作，通过隐式转换可以直接使用

| 基本类型 | 富包装                    |
| -------- | ------------------------- |
| Byte     | scala.runtime.RichByte    |
| Short    | scala.runtime.RichShort   |
| Int      | scala.runtime.RichInt     |
| Long     | scala.runtime.RichLong    |
| Char     | scala.runtime.RichChar    |
| String   | scala.runtime.RichString  |
| Float    | scala.runtime.RichFloat   |
| Double   | scala.runtime.RichDouble  |
| Boolean  | scala.runtime.RichBoolean |





