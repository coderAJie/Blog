---
title: Lua-table
categories: [Lua]
---

### 简介

table库中函数针对的几乎都是数组类型的

### 实例

- table.getn()

  ```lua
  -- #表长
  -- table.getn() #table 索引1开始 正序连续 
  -- 1.不连续			    print:3 3
  mytable={[1]="a",[2]="b",[3]="c",[5]="e"}
  mytable={[1]="a",[2]="b",[3]="c",[4]=nil,[5]="e"}
  -- 2.第一个索引不是1		 print:2 0
  mytable={[-1]="a",[0]="b",[1]="c",[2]="e"}
  mytable={[-1]="a",[0]="b",[2]="c",[3]="e"}
  -- 3.倒序				print:1
  mytable={[1]="a",[0]="b",[-1]="c",[-2]="e"}
  
  function table_leng(t)
    local leng=0
    for k, v in pairs(t) do
      leng=leng+1
    end
    return leng;
  end
  ```
  
- table.maxn()

  获取数组最大下标（数组不连续时很好用）

  若都是负数索引或者非数字索引，返回0

  ```lua
  -- print:length=2 maxn=5
  t={"a","b",[5]="e"}
  print("length="..#t)
  print("maxn="..table.maxn(t))
  ```

- table.insert(table,[pos,]value)

  不是数组类型table时使用小心，获取的length会有问题

- table.remove(table[,pos])

  删除表元素，表长度改变

  ```lua
  array = {"a","a","a","b","a","a","b"}
  for i,v in ipairs(array) do
      if v == "a" then
          table.remove(array, i)
      end
  end
  for i,v in ipairs(array) do
      print(i,v)
  end
  -- 并没有删除掉所有的a，原因是每一次删除完一个元素之后，array已经没有了那个值，再次遍历时的i其实已经是新array的i了
  --[[ print:
  1a
  2b
  3a
  4b
  ]]
  
  -- 所以这样删除 从后往前删除
  array = {"a","a","a","b","a","a","b"}
  for i=#array,1,-1 do
      if array[i] == "a" then
          table.remove(array, i)
      end
  end
  for i,v in ipairs(array) do
      print(i,v)
  end
  -- print:1b 2b
  ```

  ```lua
  -- 1.table.remove(table,pos) 返回值为对应pos的值 pos为空时删除最后一个元素 删除结束移动元素位置
  -- print:1a 2c 3d 1a 2c 3d 3 b
  mytable={"a","b","c","d"}
  n=table.remove(mytable,2)
  for k,v in pairs(mytable) do
  	print(k..v);
  end
  for k,v in ipairs(mytable) do
  	print(k..v);
  end
  print(#mytable)
  print(n)
  -- 2.nil 直接元素置空 不会移动位置 表中会有个空洞 #或者table.getn()获取长度不行
  -- print:1a 3c 4d 1a 4 nil
  mytable={"a","b","c","d"}
  mytable[2]=nil
  for k,v in pairs(mytable) do
  	print(k..v);
  end
  for k,v in ipairs(mytable) do
  	print(k..v);
  end
  print(#mytable)
  print(mytable[2])
  ```

- table.sort(table[,comp])

  排序，可以自定义排序规则

  ```lua
  array = {"egg","dophin","ai","con","body"}
  -- print:egg dophin ai con body
  
  table.sort(array)
  -- print:ai body con dophin egg
  
  table.sort(array,function(e1,e2)
  	return string.len(e1)<string.len(e2)
  end)
  -- print:ai con egg body dophin
  ```

- table.concat(…)

  以特定形式连接表中数据，只处理table中下标是数字，从1开始，连续不断开的数据

  ```lua
  t={a=1,8,"name",[9]="id","age","time"}
  for k,v in pairs(t) do
  	print(v)
  end
  -- print:8  name  age  time  1  id
  
  a=table.concat(t)
  print(a)
  -- print:8nameagetime
  -- 只处理数字下标 下标从一开始 断开就结束
  
  a=table.concat(t,"-")
  print(a)
  -- print:8-name-age-time
  -- 第二个参数为连接字符串，默认连接字符串是空串
  
  a=table.concat(t,"-",2)
  print(a)
  -- print:name-age-time
  -- 第三个参数为起始位置
  
  a=table.concat(t,"-",2,3)
  print(a)
  -- print:name-age
  -- 第四个参数为结束位置
  
  a=table.concat(t,"-",2,5)
  print(a)
  -- error
  -- 真正符合连接的数据只有4个 报错
  ```

  ```lua
  t={[1]="a",[2]="b",[3]="c"}
  a=table.concat(t)
  print(a)
  -- print:abc
  
  t={[2]="b",[3]="c"}
  a=table.concat(t)
  print(a)
  -- print:		(空串)
  ```

### 参考

https://www.jianshu.com/nb/4814025
