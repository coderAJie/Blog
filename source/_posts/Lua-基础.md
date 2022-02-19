---
title: Lua-基础
categories: [Lua]
---

### 简介

学习Lua记录

### 数据类型

```Lua
-- 1.nil 
-- 判断类型 类型名为字符串
type(x)==nil	false
type(x)=="nil"	true

-- 2.boolean
-- false,nil都为假

-- 3.number
-- 默认双精度浮点数

-- 4.string
-- 双引号或单引号 [[...]]表示一块字符串
-- 字符串长度 #string
s="helloworld";
print(#s);

-- 5.table

-- 6.function
-- 匿名函数方式传参
-- f1.lua
function testFun(tab,fun)
    for k ,v in pairs(tab) do
        print(fun(k,v));
    end
end

-- f2.lua 
tab={key1="val1",key2="val2"};
testFun(tab,
function(key,val)--匿名函数
    return key.."="..val;
end
);

-- 7.thread
-- 用于协同程序多点

-- 8.userdata
-- 自定义类型 一般C/C++的struct和指针调用

```

### 赋值

```Lua
local a,b=3,5;
local a,b=fun();
a,b=b,a
```

### 循环

```Lua
-- while
a=1;
while(a<5) do
	print(a);
	a=a+1;
end

-- for
for i=5,1,-1 do
    print(i);
end

-- for fun()
-- fun()只在循环开始前执行一次
function f(x)  
    print("fun")  
    return x*2   
end  
for i=1,f(5) do 
    print(i)  
end 
-- 输出：fun 1 2 3 4 5 6 7 8 9 10

-- for 数组 ipairs
a = {"one", "two", "three"}
for i, v in ipairs(a) do
    print(i, v)
end 

-- for table pairs

-- break 退出
```

### 函数

```Lua
-- 函数作为参数
myprint = function(param)
   print("这是打印函数 -   ##",param,"##")
end

function add(num1,num2,functionPrint)
   result = num1 + num2
   functionPrint(result)
end

myprint(10)
add(2,5,myprint)

-- 可变参数函数
function foo(...)  
    for i = 1, select('#', ...) do  -->获取参数总数
        local arg = select(i, ...); -->读取参数
        print("arg", arg);  
    end  
end  

foo(1, 2, 3, 4);  
```

### 运算符

```Lua
and or not
..(字符串连接)
#(字符串或表长度)
```

### String

```lua
s="helloworld"

-- 长度
string.len(s);					

-- 拼接
string.rep(s,3);				--string重复三次

-- 大小写转换
string.lower(s);	
string.upper(s);

-- 反转
string.reverse(s);				

-- 截取
string.sub(s,i,j);				
string.sub(s,j,-1);				---1代表最后一个 -2倒数第二个

-- 字符转换
string.char(97,98,99);			--abc
string.byte("abc",2);			--98

-- 格式化
string.format("%.4f",math.pi)	--3.1416
string.format("%02d/%02d/%04d",1,1,1990)	--01/01/1990
string.format("%s","hi");		--hi

-- 字符串匹配
string.find(s,"wo");			--6 7
string.find(s,"wo",5);			--6 7
string.find(s,"%d",1);  		--nil	%d表示查找数字
-- 返回第一个匹配字符串
string.match(s,"wo");			--wo
-- 返回迭代器函数 每次调用返回一个符合条件的字符串
string.gmatch(s,str);
attrstr = "from=world, to=Lua, name=AlbertS"
for k,v in string.gmatch(attrstr, "(%w+)=(%w+)") do 
    print(k, v) 
end		-- 返回key=value的字符串

-- 替换 返回替换后内容
string.gsub(s,"wo","-");		--hello-rld
string.gsub("aaaa","a","z",3);	--zzza
```

```lua
-- string patterns
.	:所有字符
%c	:所有控制字符
%p	:所有标点符号
%s	:所有空白字符
%w	:所有字母和数字

%a	:所有字母
%u	:所有大写字母
%l	:所有小写字母

%d	:所有十进制数字
%x	:所有十六进制数字
```

### 总结

### 参考

https://www.jianshu.com/nb/4814025
