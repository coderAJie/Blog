---
title: C#类
categories: [C#]
---

- 类成员变量封装
- 构造函数，参数化构造函数（带参）
- 析构函数
```
    using System;
    namespace LineApplication
    {
       class Line
       {
          private double length;   // 线条的长度
          public Line()  // 构造函数
          {
             Console.WriteLine("对象已创建");
          }
          ~Line() //析构函数
          {
             Console.WriteLine("对象已删除");
          }

          public void setLength( double len )
          {
             length = len;
          }
          public double getLength()
          {
             return length;
          }

          static void Main(string[] args)
          {
             Line line = new Line();
             // 设置线条长度
             line.setLength(6.0);
             Console.WriteLine("线条的长度： {0}", line.getLength());           
          }
       }
    }
```
当上面的代码被编译和执行时，它会产生下列结果：
```
    对象已创建
    线条的长度： 6
    对象已删除
```

- 静态成员
**静态成员是属于类的，非静态成员是属于对象的**
   1. static与非static最大的区别就是static类型的变量及方法在调用的时候就在内存中分配了地址，且这个地址只有一份，故static可以直接访问。而非static必需手工去实例化该类，以对象的方式去访问变量和方法。
   2. 在一个静态方法里去访问该类的非静态变量或方法，是访问不到的。由于static是属于类本身的，是在类被调用的时候，static类型就已经生成，而非static此时并没有生成，它是属于这个类的对象。故在没有实例化成对象的时候，在静态方法中访问非静态是根本找不到它们的，它不属于这个类。
   3. 在非静态方法中去访问静态是可以的。
   4. 每个类都必须有构造函数，否则此类无法实例化成对象。而我们有时定义的类可以不写它的构造函数，这是因为编译器会帮我们加上一个静态的空构造函数。这样才能实例化。也可以用静态构造函数去初始化静态变量。

区别|静态|非静态
-|-|-
调用|类.静态方法名|类 对象 = new 类的构造函数  对象.非静态方法名
初始化|静态成员是在第一次使用时进行初始化，静态构造函数只能被执行一次|非静态的成员是在创建对象的时候，非静态的构造函数可以根据需要进行多次使用
存储|静态的只有一块全局内存空间|非静态的可以有多块内存空间（副本）
释放|静态的一旦创建则在全局区一直存放，直到应用程序结束|非静态的则是由new关键字在堆中创建的。可以有多个副本。由GC进行释放。








