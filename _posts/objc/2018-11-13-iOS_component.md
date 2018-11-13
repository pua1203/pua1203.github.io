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



* 基础工具类组件：基础工具类是各个互相独立，没有任何依赖的工具组件。它们和其它的工具组件、业务组件等没有任何依赖关系。这类组件例如有：对数组，字典进行异常保护的Safe组件，对数组功能进行扩展Array组件，对字符串进行加密处理的加密组件等等。
* 基础UI组件：视图组件就比较常见了，例如我们封装的导航栏组件，Modal弹框组件，PickerView组件
* 业务工具组件：这类组件是为各个业务组件提供基础功能的组件。这类组件可能会依赖到其他的组件。例如：网络请求组件，图片缓存组件，jspatch组件等等
* **中间件（组件通讯）：**为了实现组件化开发而衍生出来的一个组件,扮演中间调度者的角色
  各个业务组件拆分出来后，组件之间的通讯、传参、回调就要考虑了，此时就需要一个组件通讯的工具类来处理。
  * 消息发送机制objc_msgSend、performSelector + runtime  API 动态生成类
* **CocoaPods远程私有库：**
  每个拆分出去的组件存在的形式都是以Pod的形式存在的，并能达到单独运行成功。
* **宿主工程：**
  宿主工程就是一个壳，在组件库中寻找这个工程所需要的组件，然后拿过来组装成一个App。





# 详细操作步骤

* 创建一个空的iOS工程项目:MainProject；

  * 初始化pod

  * 在主工程MainProject的Podfile中引入我们的业务组件

    * 使用私人pod库的需要在`Podflie`中添加source，指明你的版本库地址

    ```
    source 'https://github.com/zhangkn/Specs.git'
    
    ```

    * 如果同时使用了其他的Specs库，也要声明，例如：

      ```
        source ‘https://github.com/CocoaPods/Specs.git’
      ```

* 创建一个空业务组件工程项目：ModuleA

  * 初始化pod，初始化podspec文件

* 创建一个空工程项目:ComponentMiddleware 中间调度者

  * 初始化pod，初始化podspec文件



# See Also 

>* [iOS 组件化开发项目框架设计，结合 MVVM 设计模式 + RAC 数据绑定 + Pod 组件管理， 实现一套实战性的iOS组件化框架](https://github.com/guangqiang-liu/iOS-Component-Pro)
>  - [iOS 从零到一搭建组件化项目框架](https://juejin.im/post/5ba3cc0df265da0aac6fdaa0)
>* newpost 
>
```
/Users/devzkn/bin//newpost iOS_component 组件化 -t objc
> #原来""的参数，需要自己加上""
```

