---
title: C#结构体
categories: [C#]
---

在 C# 中，结构体是值类型数据结构。它使得一个单一变量可以存储各种数据类型的相关数据。struct 关键字用于创建结构体，结构体是用来代表一个记录。
例如，您可以按照如下的方式声明 Book 结构：
```
   struct Books
   {
      public string title;
      public string author;
      public string subject;
      public int book_id;
   };
```

####结构体 VS 类
- 类是引用类型，结构是值类型。
- 结构可带有方法、字段、索引、属性、接口和事件。
- 结构不支持继承。
- 结构可定义构造函数，但不能定义析构函数。
- 使用 New 操作符创建一个结构对象时，会调用适当的构造函数来创建结构。
- 不使用 New 操作符，只有在所有的字段都被初始化之后，对象才被使用。




