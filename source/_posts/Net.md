---
title: Net
categories: [编程杂事]
---

### 简介

关于网络的一些基础常识

---

#### 四大请求

-   GET：search，向数据库发送请求索取数据，不会增加修改数据，不会影响数据库内容
-   PUT：update，向数据库发送请求改变数据，修改的是某个具体资源的内容，不会增加数据种类
-   POST：insert，向数据库发送请求改变数据，但是会创建新的内容，多出一个东西
-   DELETE：delete，向数据库发送删除请求

**注意：** PUT主要作用于一个具体的资源上（url/xxx），POST主要是一个集合资源上（url）

---

#### 数字证书

数字证书相当于互联网通讯的驾驶执照，用来识别身份，最简单的数字证书包含一个公钥、名称以及证书授权机构的数字签名

#### 数字签名

一段报文，被发送者用私钥加密，再连同原报文一起的新的报文，就是数字签名

https://blog.csdn.net/hcm_0079/article/details/84980928

---

#### X509

X509是密码学里公钥证书的格式标准，规定了证书可以包含的信息以及格式

X509证书包含公钥、身份信息和签名信息

---

#### Http与Https

Https相当于Http+SSL，是更为安全的传输协议，传输过程中都是被加密的密文信息

Http传输的都是明文信息



