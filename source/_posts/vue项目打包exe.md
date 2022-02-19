---
title: vue项目打包exe
categories: [VUE]
---

#### 准备工作

- 安装vue

  ```
  npm install -g @vue/cli
  npm install -g @vue/cli-init
  ```

- 创建项目vue

  ```
  vue init webpack my-vue-project
  ```

- 安装electron

  ```
  npm install -g electron
  ```

- 安装electron打包工具

  ```
  npm install -g electron-packager
  ```

#### 打包EXE

1. `my-vue-project`：找到`config/index.js`文件；修改 `assetsPublicPath`的路径；文件中`dev`和`build`有两处使用到，请注意修改build处

   ```
   build: {
   	...
   	assetsPublicPath: './',
   }
   ```
   
2. `my-vue-project`：打包项目，生存文件夹`dist`

   ```
   npm run build
   ```

3. `electron`：将`dist`文件夹放在根目录，修改`main.js`文件，删除`index.html`文件

   ```
   mainWindow.loadFile('dist/index.html')
   ```

4. `electron`：执行命令运行查看运行效果

   ```
   npm run start
   ```

   此时应该可以看到vue项目变成了exe文件的形式在运行

5. `electron`：下载打包所需的依赖

   ```
   npm install electron-packager --save-dev
   ```

6. `electron`：打开`package.json`，在`scripts`中添加打包命令

   ```
   "scripts": { 
   	"start": "electron .", 
   	"packager": "electron-packager ./ App --platform=win32 --arch=x64 --overwrite"//此处为添加命令
   }
   ```

   如果你想修改最后打包出来的exe文件图标，类似于favicon，或者EXE的名字，可以设置 packager 的指令内容为，icon的路径自己调整下，更多配置内容请查阅文档： 

   ```
   "packager": "electron-packager ./ YOUR_APP_NAME --platform=win32 --arch=x64 --icon=./dist/favicon.ico --overwrite" 
   ```

7. `electron`：打包项目

   ```
   npm run packager
   ```

   到此，就生成了EXE的可执行文件，但是是一个文件夹，需要进行整个文件夹的压缩封装

#### 生成EXE安装程序

 InnoSetup下载、安装、打包

 [开源Inno Setup官网下载、安装、打包教程（官网安装向导中文语言包） - 奔跑的简单 - 博客园 (cnblogs.com)](https://www.cnblogs.com/benpaodejiandan/p/7081011.html) 
