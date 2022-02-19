---
title: Lua-io
categories: [Lua]
---

### 简介

没有特殊情况，所有IO函数在失败的情况下返回nil（第二个参数一般是错误信息

）

### 实例

- io.open(filename[,mode])

  出错返回nil及错误信息 正确返回文件编号 mode为打开方式

  - “r”：只读，文件必须存在，默认打开方式
  - “r+”：只读，文件必须存在，读取从头开始，写入从头开始，保留原内容
  - “w”：只写，文件存在清空，不存在创建，写入从头开始
  - “w+”：只写，文件存在清空，不存在创建，读取从头开始，写入从头开始
  - “a”：附加方式打开只写文件，文件不存在创建，写入从尾开始，保留原内容
  - “a+”：附加方式打开可读写文件，文件不存在创建，写入从尾开始，保留原内容

  ```lua
  -- 注意：mode有引号 以下纯打开不进行任何操作文件亿被清空
  a,b=io.open("test1.txt","w+")
  print(a,b)
  ```

- io.close([file])

  关闭文件，成功true，参数并不是文件名

  其他写法：file:close() 

  ```lua
  -- print:true
  a,b=io.open("test1.txt","w+")
  --c=io.close("test1.txt")	--文件名报错
  c=io.close(a)
  print(c)
  ```

- io.input([file]) 

  参数可以为文件名或者文件，将其设为默认的输入文件，不填参数默认的是命令行界面

  ```lua
  -- 文件名参数 文件内容作为默认输入文件
  io.input("111.txt")
  a=io.read("*l")
  print(a)
  
  -- 文件参数 
  f=io.open("111.txt")
  io.input(f)
  a=io.read("*l")
  print(a)
  
  -- 命令行 默认的io.input()输入文件
  a=io.read("*l")
  print(a)
  ```

- io.output() 

  参数文件名，将其设为默认的输出文件，不填参数默认的是命令行界面（io.stdout）

  ```lua
  -- 注意：最好先确定输入文件以及输出文件 再进行读取操作
  -- 命令行界面io.stdout
  io.output(io.stdout)
  a=io.read("*l")
  b=io.write("name:"..a)
  
  -- 文件名
  io.output("111.txt")
  a=io.read("*l")
  b=io.write("name:"..a)
  ```

- io.read(…) 

  根据格式读取内容 读不到返回nil 默认以`*l`的形式读取

  其他写法：file:read() 这样可以不用设置默认输入文件

  读取完一次之后 当前位置会到读取末尾 下次读取继续继续 若是关闭文件重新读取 则从头开始

  - “n”：读取一个数字 唯一返回数字而不是字符串的读取格式
  - “a”：从当前位置读取余下的所有内容，如果在文件尾，则返回空串
  - “l”：读取下一行内容，在文尾则返回nil
  - number：读取number个字符的字符串，number=0则返回空串，在文尾则返回nil

  ```lua
  -- 111.txt
  1start
  2line2
  3line3
  4line4
  5line5
  6end
  ```

  ```lua
  -- 读取完当前位置改变 文件关闭重新读取当前位置从头开始
  -- print:1start	2line2	1start
  file=io.input("111.txt")
  a=io.read("*l")
  print(a)
  
  b=io.read("*l")
  print(b)
  
  io.close(file)
  
  io.input("111.txt")
  c=io.read("*l")
  print(c)
  ```

  ```lua
  -- b的10个字符包括一个换行符 c=nil 
  --[[ print:
  a:1start
  b:2line2
  3li
  nil
  d:ne3
  4line4
  5line5
  6end
  ]]
  file=io.open("111.txt","r")
  a=file:read("*l")
  print("a:"..a)
  
  b=file:read(10)
  print("b:"..b)
  
  c=file:read("*n")
  print(c)
  
  d=file:read("*a")
  print("d:"..d)
  ```

- io.write(…)

  可以有多个参数，每个参数必须是字符串或者数字，其他类型使用tostring或string.format()写入 

  其他写法：file:write() 这样可以不用设置默认输出文件

  ```lua
  --[[ print:
  hello
  hello
  world
  world
  
  ]]
  file=io.open("111.txt","a")
  io.output(file)
  io.write("hello\n")
  io.write("hello\n")
  
  file:write("world\n")
  file:write("world\n")
  ```

- file:seek(whence,offset)

  控制读写指针，设置获取文件位置，返回值为最终文件位置，offset表示偏移默认0，whence表示不同模式

  - “set”：文件头开始
  - “cur”：从当前开始（默认）
  - “end”：文件尾开始

  ```lua
  -- offset可以为负数 file:seek("end")返回值正好是文件大小
  --[[
  n:0		a:1start
  n:3		a:art
  2l
  n:13	a:2
  3lin
  n:41	a:end
  ]]
  file=io.open("111.txt","a+")
  n=file:seek("set");
  a=file:read(6)
  print("n:"..n.."	a:"..a)
  
  n=file:seek("set",3);
  a=file:read(6)
  print("n:"..n.."	a:"..a)
  
  n=file:seek("cur",3);
  a=file:read(6)
  print("n:"..n.."	a:"..a)
  
  n=file:seek("end",-3);
  a=file:read(6)
  print("n:"..n.."	a:"..a)
  ```

  ```lua
  -- 关于a+方式，只从内容尾开始写入，seek当前位置是正确的，但执行写入时直接继续在尾部写，并不在当前位置写入
  file=io.open("111.txt","a+")
  a=file:write("!-!")
  n=file:seek("cur",-10)
  b=file:write("!-!")
  ```

  ```lua
  -- print:!!---!
  file=io.open("111.txt","w")
  file:seek()
  file:write("!-!")
  file:seek("cur",-2)
  file:write("!---!")
  ```

- io.type()

  判断文件描述符的状态 是一个打开的文件返回字符串“file”，是个关闭的文件返回字符串“closed file”，是无效文件描述符返回nil

  ```lua
  -- print:file	closed file		nil
  file=io.open("111.txt")
  print(io.type(file))
  
  file:close()
  print(io.type(file))
  
  print(io.type("Test"))
  ```

- io.lines([filename])

  只读方式打开文件 返回一个迭代函数，每次调用都返回文件中新的一行，当读取到结尾时，返回nil并自动关闭文件

  因为是只读方式，所以最好先检测一下是否存在

  其他写法：file:lines() 这种写法结束时不会自动关闭

  ```lua
  --[[ print:
  1start
  2line2
  3line3
  4line4
  5line5
  6end
  ]]
  func=io.lines("111.txt")
  print(func())
  print(func())
  
  for line in func do
  	print(line)
  end
  ```

  ```lua
  -- 注意：输出最后io.type=file 说明文件在最后没有关闭，这个是io.lines(filename)和file:name的区别
  --[[ print:
  1start
  2line2
  3line3
  4line4
  5line5
  6end
  file
  ]]
  file=io.open("111.txt")
  for line in file:lines() do
  	print(line)
  end
  print(io.type(file))
  file:close()
  ```

### 参考

https://www.jianshu.com/nb/4814025


