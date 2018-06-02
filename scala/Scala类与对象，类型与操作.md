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

