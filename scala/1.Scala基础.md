#Scala基础

## 变量声明和使用

```scala
val a = 10
var b = 20
```

## 函数使用

```scala
def hello(a:Int,b:Int):Int{
    if(a > b)
    	a
    else
    	b
}
```

## while循环

```scala
var i = 0;
while(i <10){
	print(i)
	i += 1
}
```

## for循环

```scala
//函数式语言的主要特征就是：函数是头等结构
val a = List(1,2,3)
a.foreach(b => println(b))//括号中传入的是函数字面量

//for循环的例子
for(b <- a){
    println(b+1)
}
```

### 函数字面量的语法格式

```scala
//函数字面量语法
(a:Int,b:Int) => x + y

//如果函数字面量只有一行，并且只有一个参数，那么可以不写参数，直接写执行语句，例如：
args.foreach(println)

//复杂的写法：
val a = List(1,2,3)
a.foreach(b => {
	println(b);
	println(b+2);
})
```

## 数组（array）、列表（list）、元组（tuple）、集（set）、映射（map）

###数组（Array）

```scala
val arr = new Array[String](3)
//这里的arr(0),实际上是对数组的apply()方法的调用，arr(0)等同于 arr.apply(0)
arr(0) = "Hello"
arr(1) = "World"
arr(2) = "heihei"
//使用foreach
arr.foreach(println)
//使用for-i，这里的to是Int的一个方法，带有一个参数，如果是这种情况，可以省略点和括号，直接调用方法，+，-这些都是方法名
for(i <- 0 to 2)
	println(arr(i))
//使用for-i,效果与上边等同
for(i <- 0 to arr.length-1)
	println(arr(i))
```

#### 给数组赋值的方式

```scala
//更简洁的赋值方式
val a = Array("a","b","c")
```

### 列表（List），不可变，包含同类元素

```scala
//列表类似于java的String，一旦赋值就不可变了
val li = List(1,2,3)
//两个列表合并：
val a1 = List(1,2,3)
val a2 = List(4,5)
val a3 = a1 ::: a2

//将新元素加入到列表中，加入到列表的最前端,元素在前边
//以冒号结尾的方法，例如这里的::, 这个::其实是a1的方法
val a4 = 6 :: a1

//Nil是空列表的简写，所以可以用cons操作符把所有元素都串起来，并以Nil结尾来定义新的列表
val a5 = 1 :: 2 :: 3 :: Nil

//list 没有提供append方法，可以使用ListBuffer，其他方法看文档
```

###元组（tuple），不可变，包含不同类元素

```scala
//定义：
val pair = (100,"Hello")
//获取元素,调用_N方法,N从1开始
val a = pair._1 //100
val b = pair._2 //"Hello"
```

### 集（Set） 和 映射（Map）

#### Set

```scala
//Set有可变与不可变之分，默认是不可变的
//声明（默认不可变的）：
var aSet = Set("a","b")
aSet += "c"   //会返回一个新的Set，因为当前这个set是不可变的
println(aSet.contains("d"))

//声明可变的Set:
import scala.collection.mutable.Set
val bSet = Set("a","b")
bSet += "c"
println(bSet)

//指明具体Set类型：
import scala.collection.immutable.HashSet
val hashSet = HashSet("Tomatoes","Chilies")
println(hashSet + "Coriander")
```

#### Map

```scala
//同样有可变与不可变之分
//默认是不可变的：
var aMap = Map[Int,String](1->"a",2->"b")
aMap += (3->"c")//会产生一个新的Map并重新赋值给aMap
aMap += (4->"d")//同上

//可变Map：
import scala.collection.mutable.Map
val bMap = Map(1->"a",2->"b")
bMap += (3->"c")//添加元素
println(bMap(1))


```

## 函数式编程风格

* 使用val
* 避免函数的副作用，比如在函数中产生打印语句等
* scala是指令式和函数式混合的编程语言，两种方式都可以使用，不过函数式要更简单。



## 读取文件内容

```scala
import scala.io.Source

def widthOfLength(s:String) = s.length.toString.length

if(args.length > 0){
    val lines = Source.fromFile(args(0)).getLines.toList
    
    val longestLine = lines.reduceLeft(
    	(a,b) => if(a.length > b.length) a else b
    )
    
    val maxWidth = widthOfLength(longestLine)
    
    for(line <- lines){
        val numSpaces = maxWidth - widthOfLength(line)
        val padding = " " * numSpaces
        println(padding + line.length + " | " + line)
    }
}
else
	Console.err.println("Please enter filename")
```



