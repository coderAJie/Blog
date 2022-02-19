---
title: vue项目打包apk
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

- 安装cordova相关

  ```
  npm install -g cordova
  ```



#### cordova项目内打包

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

3. `cordova`：创建cordova项目，new-cordova是项目名称，com.my.vue2apk是包名，vue2apk是程序的标题

   ```
   cordova create new-cordova com.my.vue2apk vue2apk
   ```

4. `cordova`：将刚才在vue项目中打包生成的dist文件夹下面的index.html和static文件夹复制到www文件夹下面，将原先www文件夹下面的所有文件删除。
   
5. `cordova`：打包cordova项目

   ```
   cordova platforms add android --save
   ```

6. `cordova`：生成apk文件

   ```
   cordova build android
   ```

   此时生成的文件就可以正常在模拟器安装，但是缺少了签名，之后需要进行签名生成重新打包，在此不做深究

#### 引用

>  [前端VUE项目打包成安卓APP_氵易风灬的博客-CSDN博客_vue打包成app](https://blog.csdn.net/qq_21963133/article/details/88546086) 
