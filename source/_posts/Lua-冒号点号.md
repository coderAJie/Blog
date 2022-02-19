---
title: Lua-冒号点号
categories: [Lua]
---

### 简介

关于冒号（:）与点号（.）

冒号自带隐藏self，点号不带self，方法用冒号

### 示例

```
class={x=1}

--冒号+方法
function class:print()
	print(self.x);
end
--点号+self
function class.print(self)
	print(self.x);
end

--冒号调用
class:print();
--点号调用
class.print(class);
```

