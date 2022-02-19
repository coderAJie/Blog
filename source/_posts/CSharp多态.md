---
title: C#多态
categories: [C#]
---

###静态多态
- 函数重载
对相同函数名的函数有多个定义，需要参数列表中的参数类型或者个数不同
```
    void print(int i)
    {
       Console.WriteLine("Printing int: {0}", i );
    }

    void print(double f)
    {
       Console.WriteLine("Printing float: {0}" , f);
    }
```
- 运算符重载
重载运算符是特殊名称的函数，通过关键字 operator 后跟运算符的符号来定义。与其他函数一样，重载运算符有返回类型和参数列表。
下面的函数为用户自定义的类 Box 实现了加法运算符（+）。它把两个 Box 对象的属性相加，并返回相加后的 Box 对象。
```
    public static Box operator+ (Box b, Box c)
    {
       Box box = new Box();
       box.length = b.length + c.length;
       box.breadth = b.breadth + c.breadth;
       box.height = b.height + c.height;
       return box;
    }
```
###动态多态
- 抽象类
   1. 您不能创建一个抽象类的实例。
   2. 您不能在一个抽象类外部声明一个抽象方法。
- 虚方法
当有一个定义在类中的函数需要在继承类中实现时，可以使用虚方法。虚方法是使用关键字 virtual 声明的。虚方法可以在不同的继承类中有不同的实现。
