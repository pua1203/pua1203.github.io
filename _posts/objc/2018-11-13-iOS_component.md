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



#### **在组件化中重要的是让组件职责单一，职责单一的重要标志之一就是没有组件间的循环依赖。**



* 采用组件化，是为了组件能单独开发，能单独开发, App就能快速集成。
  * 要让组件能单独开发，`组件必须职责单一`，对于代码中已有模块，就需要用到重构和解耦的技术，所以重构和解耦是过程。目的是去除循环依赖。
    * A、B组件循环依赖就是设计有问题，要么应该重构A、B让依赖单向；要么应该抽离一个共用组件C，让A、B组件都只依赖于C。



![image](https://ws1.sinaimg.cn/large/af39b376gy1fx6h86htnvj20rs0jvtev.jpg)



![image](https://ws1.sinaimg.cn/large/af39b376gy1fx6h9iubugj20rs086ack.jpg)





#### 组件化必备的工具使用: `要解除循环依赖，引入包管理技术cocoapods会让我们更有效率。pod不允许组件间有循环依赖，若有pod install时就会报错。`



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

  * 主工程中添加一个按钮事件，这个事件是点击 `push 到业务组件`()

    ```
        UIViewController *VC = [[CTMediator sharedInstance] EleInvoice_ViewControllerWithCallback:^(NSString *result) {
            NSLog(@"resultA: --- %@", result);
        }];
        [self.navigationController pushViewController:VC animated:YES];
    
    ```

* 创建一个空业务组件工程项目：Module

  * 初始化pod，初始化podspec文件

* [创建一个空工程项目: ModuleCategory，这个工程是对应业务组件的一个分类工程。](https://github.com/guangqiang-liu/iOS-Component-Pro/blob/master/Pods/ModuleBCategory/ModuleB-Category/Category/CTMediator%2BModuleB.m)

  * 然后我们初始化pod，初始化podspec文件。

  * 只对外暴露了两个文件。这两文件是上面的中间调度者Mediator的分类，也就是说是中间件的分类

    ```
    #import "ComponentScheduler+ModuleB.h"
    
    @implementation ComponentScheduler (ModuleB)
    
    - (UIViewController *)ModuleB_viewControllerWithCallback:(void(^)(NSString *result))callback {
        NSMutableDictionary *params = [[NSMutableDictionary alloc] init];
        params[@"callback"] = callback;
        return [self performTarget:@"ModuleB" action:@"viewController" params:params shouldCacheTarget:NO];//上面的performTarget:action:params:shouldCacheTarget 函数是中间件提供的函数。因为ModuleBCategory 是 ComponentScheduler(中间件)的分类文件，所以可以调用到这个函数啦。在ModuleBCategory 工程中需要引用到了中间件工程所以我们需要在ModuleBCategory 的Podfile文件中引用 中间件组件ComponentScheduler
    }
    @end
    
    ```

  * 分类实现非常的简单，就是对外暴露一个函数，然后执行`[self performTarget:@"ModuleB" action:@"viewController" params:params shouldCacheTarget:NO];` ，并将执行的返回值返回出去。

  * 这个分类的作用你可以理解为我们提前约定好Target的名字和Action的名字，因为这两个名字中间件组件中Mediator会用到。

* 创建一个空工程项目:CTMediator 中间调度者,使用objc_msgSend、performSelector + runtime  API 动态生成target，执行action。

  * 初始化pod，初始化podspec文件

  * [ `performTarget:action:params:shouldCacheTarget` 吧，这个是中间件的核心函数](https://github.com/guangqiang-liu/iOS-Component-Pro/blob/master/Pods/CTMediator/CTMediator/CTMediator/CTMediator.m#L68)



![image](https://ws1.sinaimg.cn/large/af39b376gy1fx6gupr95lj20sg0lcto7.jpg)

# See Also 

>* [iOS 组件化开发项目框架设计，结合 MVVM 设计模式 + RAC 数据绑定 + Pod 组件管理， 实现一套实战性的iOS组件化框架](https://github.com/guangqiang-liu/iOS-Component-Pro)
>
>  - [iOS 从零到一搭建组件化项目框架](https://juejin.im/post/5ba3cc0df265da0aac6fdaa0)
>
>  - [iOS MVVM开发模式 配合 RAC 信号绑定框架让开发更有趣](https://github.com/guangqiang-liu/iOS-MVVM-RAC)
>
>* newpost 
>
```
/Users/devzkn/bin//newpost iOS_component 组件化 -t objc
> #原来""的参数，需要自己加上""
```

