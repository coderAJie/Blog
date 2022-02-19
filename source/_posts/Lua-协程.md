---
title: Lua-协程
categories: [Lua]
---

### 简介

### 示例

```lua
co=coroutine.create(
	function()
		print("hi");
	end
)
print(coroutine.status(co));

coroutine.resume(co);
print(coroutine.status(co));
--[[print:
suspended
hi
dead
]]
```

```lua
co=coroutine.create(
	function()
		for i=1,2 do
			print("hi");
			coroutine.yield();
		end
	end
)
coroutine.resume(co);
print(coroutine.status(co));

coroutine.resume(co);
print(coroutine.status(co));

coroutine.resume(co);
print(coroutine.status(co));

coroutine.resume(co);
print(coroutine.status(co));
--[[print:
hi
suspended
hi
suspended
dead
dead
]]
```

#### 参数及返回值

- create：返回coroutine，参数是函数
- resume：返回bool值 
- yield：挂起
- status：返回状态
- wrap：返回一个函数，调用这个函数时就开始执行，相当于create+resume
- running：返回运行的coroutine

```lua
-- bool + 函数返回参数
co=coroutine.create(
	function()
		return 4,5;
	end
)
print(coroutine.resume(co,1,2,3));
--[[print:
true 4 5
]]
```

```lua
-- bool + 传入参数多少
co=coroutine.create(
	function(a,b)
		print(a,b);
		coroutine.yield();
	end
)
print(coroutine.resume(co,1,2,3));
--[[print:
1 2 
true
]]
```

```lua
-- bool + yield所有参数
co=coroutine.create(
	function(a,b)
		print(a,b);
		coroutine.yield(a+b,a-b,a*b,a/b);
	end
)
print(coroutine.resume(co,1,2,3));
--[[print:
1 2
true 3 -1 2 0.5			--所有传递给yield的参数都将返回
]]
```

```lua
-- wrap
co=coroutine.wrap(
	function(a)
		return 2*a;
	end
)
c=co(1);
print(c);
--[[print:
2
]]
```



