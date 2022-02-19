---
title: C#数组
categories: [C#]
---

###创建
1. 一维数组
   - int[] n  =new int[10];  //不赋值
   - int[] n = {1,2,3};         //赋值
2. 二维数组
   - int[,] = new int[2,3];
3. 交错数组
   - int[][] = new int[2][];
   - int[][] = {new int[]{1,2},new int[]{1,2,3}};
4. 参数数组（params）
```
    using System;
    namespace ArrayApplication
    {
       class ParamArray
       {
          public int AddElements(params int[] arr)
          {
             int sum = 0;
             foreach (int i in arr)
             {
                sum += i;
             }
             return sum;
          }
       }
    
       class TestClass
       {
          static void Main(string[] args)
          {
             ParamArray app = new ParamArray();
             int sum = app.AddElements(512, 720, 250, 567, 889);
             Console.WriteLine("总和是： {0}", sum);
             Console.ReadKey();
          }
       }
    }
```

###方法
Array 类是 C# 中所有数组的基类，它是在 System 命名空间中定义。Array 类提供了各种用于数组的属性和方法。

方法|描述
-|-
Reverse()|逆转数组
Sort()|排序数组
