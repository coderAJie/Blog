---
title: Lua-os
categories: [Lua]
---

### 简介

### 实例

- os.clock(time) 返回执行该程序CPU花去的时钟秒数

  ```lua
  start=os.clock()
  while true do
  	if os.clock()-start>3 then
  		start=os.clock()
  		print("111")
  	end
  end
  ```

- os.date(time) 返回时间字符串 格式化形式多

  ```lua
  -- 本地时间
  local timetable = os.date("*t", os.time());   
  for i, v in pairs(timetable) do
        print(i, v);
  end
  -- ！格林尼治时间
  local utimetable = os.date("!*t", os.time()); 
  for i, v in pairs(utimetable) do
        print(i, v);
  end
  ```

- os.time([table]) 返回当前系统的时间

  ```lua
  -- print:1540433633		0	01/01/70 08:00:00	01/01/70 00:00:00
  -- 北京时间的1970-1-1 08:00:00是0时区时间的1970-1-1 00:00:00
  print(os.time())
  
  t={year=1970,month=1,day=1,hour=8}
  print(os.time(t))
  
  print(os.date("%c",os.time(t)))
  print(os.date("!%c",os.time(t)))
  ```

- os.difftime(t1,t2) 时间差值 返回秒数

- os.execute([command]) 调用系统的很多函数 可以复制文件 暂停 等等

- os.exit() 退出程序

- os.getenv(name) 查询系统环境变量 程序路径 系统盘符

  ```lua
  print(os.getenv("SystemRoot"))          -- 系统根目录
  print(os.getenv("WoXiaXieDe"))          -- 我乱写的
  print(os.getenv("ALLUSERSPROFILE"))     -- 所有“用户配置文件”的位置
  print(os.getenv("alluserSpRoFilE"))     -- 所有“用户配置文件”的位置
  print(os.getenv("COMPUTERNAME"))        -- 计算机的名称
  
  print(os.getenv("COMSPEC"))             -- 命令行解释器可执行程序的准确路径
  print(os.getenv("HOMEDRIVE"))           -- 连接到用户主目录的本地工作站驱动器号
  print(os.getenv("HOMEPATH"))            -- 用户主目录的完整路径
  print(os.getenv("NUMBER_OF_PROCESSORS"))-- 安装在计算机上的处理器的数目
  print(os.getenv("OS"))                  -- 操作系统的名称
  
  print(os.getenv("PROCESSOR_LEVEL"))     -- 计算机上安装的处理器的型号
  print(os.getenv("PATHEXT"))             -- 连接到用户主目录的本地工作站驱动器号
  print(os.getenv("PROCESSOR_REVISION"))  -- 处理器修订号的系统变量
  print(os.getenv("TEMP"))                -- 临时目录
  print(os.getenv("SYSTEMDRIVE"))         -- 系统根目录的驱动器
  ```

- os.remove(file) 删除文件

- os.rename(oldname,newname) 重命名

### 参考

https://www.jianshu.com/nb/4814025
