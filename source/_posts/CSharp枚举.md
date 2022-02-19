---
title: C#枚举
categories: [C#]
---

```
    enum State
    {
        Idle,
        Run,
        Die,
        Attack
    }
```

```c#
    //1
	int index = (int)State.Run;

	//Run
    string s = Enum.GetName(typeof(State), 1);

	//Int32
    Type t = Enum.GetUnderlyingType(typeof(State));

	//Idle Run Die Attack
    string[] ss = Enum.GetNames(typeof(State));
    foreach (var item in ss){}

	//Idle Run Die Attack
    Array a = Enum.GetValues(typeof(State));
    foreach (var item in a){}
```
