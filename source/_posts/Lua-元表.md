---
title: Lua-元表
categories: [Lua]
---

### 简介

模块库类似一个封装库，存放公用代码，以api接口形式被其他调用

```Lua
-- module.lua模块
-- 定义模块
module={}

-- 定义常量
module.a=1
-- 定义公有函数
function module.fun1()
    print("public");
end
-- 定义私有函数
local function module.fun2()
    print("private");
end
-- return
return module


-- test.lua调用
require("module")
module.fun1()
```

### 元表

#### 元表（metatable）提供两个table之间的操作

- set：将table设置为元表 （若元表存在_metatable键值 则设置失败）

  ```Lua
  mytable={}		--普通表
  metatable={}	--元表
  setmetatable(mytable,metatable)	--设置为元表
  ```

- get：获取对象的元表

  ```Lua
  getmetatable(mytable)
  ```

#### 元方法

- `__index`：访问表，表中没有对应值时，去元表的`__index`中找（`__table`可以是表包含很多）

  ```lua
  t1={a=1,b=2};
  t2={};
  setmetatable(t1,t2);
  print(t1.c);
  
  -- 包含表
  t3={a=1,b=2};
  t4={__index={c=3}};
  setmetatable(t3,t4);
  print(t3.c);
  
  -- 包含函数(function注意包含t6参数)
  t5={a=1,b=2};
  t6={__index=
  	function(t6,key)
  		if(key=="c") then
  			return 3;
  		else
  			return nil;
  		end
  	end
  };
  setmetatable(t5,t6);
  print(t5.c);
  
  -- 或者写法
  t7={a=1,b=2};
  setmetatable(t7,{__index={c=3}});
  print(t7.c);
  ```

- `__newindex`：更新表，赋值对应键值，若没有，就会去元表的`__newindex`中找

  ```lua
  m={d=4};
  meta={__newindex=m};
  mytable={a=1,b=2};
  setmetatable(mytable,meta);
  mytable.c=3;	-- 将c键值加到m中
  print(mytable.c,m.c,mytable.d,m.d);	-- nil 3 nil 4
  
  m={d=4};
  meta={__newindex=m,__index=m};
  mytable={a=1,b=2};
  setmetatable(mytable,meta);
  mytable.c=3;	-- 将c键值加到m中 此刻m含有c键值
  print(mytable.c,m.c,mytable.d,m.d);	-- 3 3 4 4
  
  -- 或者写法
  m={d=4};
  mytable={a=1,b=2};
  setmetatable(mytable,{__newindex=m,__index=m});
  
  mytable.c=3;
  print(mytable.c,m.c,mytable.d,m.d);
  ```

- rawget rawset：rawget可以直接获取索引实际值，不通过`__index`元方法 rawset可以直接对表中索引赋值，不通过`__newindex`元方法

  ```lua
  -- rawget调用方式不同
  t7={a=1,b=2};
  setmetatable(t7,{__index={c=3}});
  --print((t7.c));
  print(rawget(t7,c));
  
  -- rawset赋值方式不同
  m={};
  mytable={a=1,b=2};
  setmetatable(mytable,{__newindex=m});
  --mytable.c=3;
  rawset(mytable,"c",3);
  print(mytable.c,m.c);
  ```

- 操作符：就是对应符号对应的”__名字“，主要还是对应操作符后面写的方法

  ```lua
  mytable={a=1,b=2,c=3};
  meta={__add=
  	function(first,second)
  		for k,v in pairs(second) do
  			table.insert(first,v);
  		end
  		return first;					-- 元表就是一个操作
  	end
  }
  mytable = setmetatable(mytable,meta)
  
  secondtable={d=4,e=5,f=6};
  mytable=mytable+secondtable;
  
  for k,v in pairs(mytable) do
  	print(v);
  end
  
  --[[ 对应其他的操作
  +		=>	__add
  -(减号)  =>  __sub	
  *		=>	__mul
  /		=>	__div
  %		=>	__mod
  -(负号)  =>  __unm
  ..		=>	__concat
  ==		=>	__eq
  <		=>	__lt
  <=		=>	__le
  ]]
  ```

- __call：在Lua调用一个值时调用，就是调用每个值可能要进行统一操作

  ```lua
  mytable={"111","222"};
  meta={__call=
  	function(first,a)
  		return("id="..a.." is "..first[a]);
  	end
  }
  mytable=setmetatable(mytable,meta)
  
  print(mytable(2));
  ```

- __tostring：修改表的输出行为

  ```lua
  mytable={"111","222"};
  meta={__tostring=
  	function(first)
  		for k,v in ipairs(first) do
  			return("id="..k.." is "..v);
  		end
  	end
  }
  setmetatable(mytable,meta)
  
  print(mytable);
  ```

### 总结

- meta元表代表的是一种操作，放在其他地方也这样写，与具体的表无关
- meta元表可以做很多操作，命名不同，具体做什么在function里面实现
- meta元表可以做很多初始化或者类似构造函数的功能，面向对象编程
- pairs：是迭代器的元方法，__pairs

### 参考

https://www.jianshu.com/nb/4814025
