---
layout: post
title: iOS_component
date: 2018-11-13
tag: objc
site: https://zhangkn.github.io
catalog: true
author: kunnan
subtitle: 组件化
---



# 前言



#### 组件化必备的工具使用



* [制作CocoaPods远程私有库，将其发不到公司的gitlab或GitHub，使工程能够Pod下载下来。](https://kunnan.github.io/2017/03/10/making_private_cocoapods/)



####  模块拆分

![image](https://ws1.sinaimg.cn/large/af39b376gy1fx6eutslo0j20rs0kuwtb.jpg)



* **中间件（组件通讯）：**
  各个业务组件拆分出来后，组件之间的通讯、传参、回调就要考虑了，此时就需要一个组件通讯的工具类来处理。
* **CocoaPods远程私有库：**
  每个拆分出去的组件存在的形式都是以Pod的形式存在的，并能达到单独运行成功。
* **宿主工程：**
  宿主工程就是一个壳，在组件库中寻找这个工程所需要的组件，然后拿过来组装成一个App。

# See Also 

>* newpost 
>
```
/Users/devzkn/bin//newpost iOS_component 组件化 -t objc
> #原来""的参数，需要自己加上""
```

