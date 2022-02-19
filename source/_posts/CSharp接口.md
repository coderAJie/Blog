---
title: C#接口
categories: [C#]
---

继承接口后，我们需要实现接口的方法 MethodToImplement() , 方法名必须与接口定义的方法名一致
```
    using System;

    interface IMyInterface
    {
        // 接口成员
        void MethodToImplement();
    }

    class InterfaceImplementer : IMyInterface
    {
        static void Main()
        {
            InterfaceImplementer iImp = new InterfaceImplementer();
            iImp.MethodToImplement();
        }

        public void MethodToImplement()
        {
            Console.WriteLine("MethodToImplement() called.");
        }
    }
```
