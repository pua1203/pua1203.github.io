---
layout: post
title: Code_Signing
date: 2018-09-20
tag: objc
site: https://zhangkn.github.io
catalog: true
author: kunnan
subtitle: 摘要、Public-key cryptography、Keychain Access、AppID、Provisioning Profile、entitlements 以及 p12；
---



# 前言

本文主要是为了回顾一下iOS正向开发的基础知识。现在Xcode关于证书的配置越来越自动化。

了解签名相关的概念有助于自己写自动打包的脚本，或者重新签名其他app。





#### Public-key cryptography



* 一個是公开密钥，另一個是私有密钥；一個用作加密的時候，另一個則用作解密。





#### 数字签名

* 类似于生活中的购物信用卡签名，主要用于鉴别身份的真实性

* 数字签名就是将公钥密码反过来使用。签名者把数据（通常是散列值）用私钥加密，用公钥将加密的数据解密并比对。

  ![image](https://ws2.sinaimg.cn/large/af39b376gy1fvg2i6fxgxj20hf0i2jtk.jpg)



#### Keychain Access



keychain 的证书助手来申请公私钥。生成的 `CertificateSigningRequest` 就是公钥，私钥保存在 keychain 中。

#### AppID、Provisioning Profile、entitlements 、 p12



* **AppID** 是由 TeamID 和 BundleID 组合而成，类似于 `A1B2C3D4.com.domain.appName`形式
* **Entitlements** 包含了 App 关于 iCloud、Push、backgroundMode 以及`是否可以调试`等权限信息。



* **Provisioning Profile** 里边包含了数字签名信息、授权设备列表信息、Entitlements 等信息以及这些信息的签名。
* p12   是由cer 转换而得的一种文件格式，里边包含了我们的私钥信息以及符合 `X.509` 标准的公钥。

#  code signing

#### 双层签名

- 两对公私钥

  * 申请证书的时候，在 Mac 开发机器生成一对公私钥，这里称为公钥L，私钥L。
    * 对应的是 keychain 里的 “从证书颁发机构请求证书”，这里就本地生成了一对公私钥，保存的 CertificateSigningRequest 就是公钥，私钥保存在本地电脑里。
      * 把公钥 L 传到苹果后台，用苹果后台里的私钥 A 去签名公钥 L。得到一份数据包含了公钥 L 以及其签名，把这份数据称为AcountCertificateSigningRequest证书。这个证书可用于申请appID
  * 苹果自己有固定的一对公私钥，私钥在苹果后台，公钥在每个 iOS 设备上。这里称为公钥A，私钥A。

- 在苹果后台申请 AppID，配置好设备 ID 列表和 APP 可使用的权限，再加上一步的AcountCertificateSigningRequest证书，组成的数据用私钥 A 签名，把数据和签名一起组成一个 Provisioning Profile 文件

  * `对应把 CertificateSigningRequest 传到苹果后台生成证书，并下载到本地。这时本地有两个证书，一个是第 1 步生成的，一个是这里下载回来的，keychain 会把这两个证书关联起来，因为他们公私钥是对应的，在XCode选择下载回来的证书时，实际上会找到 keychain 里对应的私钥去签名。这里私钥只有生成它的这台 Mac 有，如果别的 Mac 也要编译签名这个 App 怎么办？答案是把私钥导出给其他 Mac 用，在 keychain 里导出私钥，就会存成 .p12 文件，其他 Mac 打开后就导入了这个私钥。`
  * 在苹果网站上操作，配置 AppID / 权限 / 设备等，最后下载 Provisioning Profile 文件。

- 在开发时，编译完一个 APP 后，用本地的私钥 L 对这个 APP 进行签名，同时把第上步得到的 Provisioning Profile 文件打包进 APP 里，文件名为 embedded.mobileprovision，把 APP 安装到手机上。

  * `XCode 会通过下载回来的证书（存着公钥），在本地找到对应的私钥（第一步生成的），用本地私钥去签名 App，并把 Provisioning Profile 文件命名为 embedded.mobileprovision 一起打包进去。这里对 App 的签名数据保存分两部分，Mach-O 可执行文件会把签名直接写入这个文件里，其他资源文件则会保存在 _CodeSignature 目录下。`

- 在安装时，iOS 系统取得证书，通过系统内置的公钥 A，去验证 embedded.mobileprovision 的数字签名是否正确，里面的证书签名也会再验一遍。

- 确保了 embedded.mobileprovision 里的数据都是苹果授权以后，就可以取出里面的数据，做各种验证，包括用公钥 L 验证APP签名，验证设备 ID 是否在 ID 列表上，AppID 是否对应得上，权限开关是否跟 APP 里的 Entitlements 对应等。

![image](https://ws2.sinaimg.cn/large/af39b376gy1fvg32y7lkej20hn0b7jsr.jpg)

* 签名是在安装流程进行校验的，越狱设备可以安装一些tweak来屏蔽签名校验
* 在app被加载到内存的时候，app store 对app的加固会被解密，因此可以利用这个时机进行[dump](https://github.com/AloneMonkey/frida-ios-dump)



# See Also 



#### 存储



> * [    MMKV——基于 mmap 的高性能通用 key-value 组件](<https://github.com/Tencent/MMKV/blob/master/readme_cn.md>)
>   * https://mp.weixin.qq.com/s/4MHgs4qpLt7krpmIp9rgRg

#### other 



>* [ishare](http://ishare.iask.sina.com.cn/u/5099ed2b0cf2c9d5dae52a41.html)
>* [xcodegen: 我是不太喜欢使用它](https://mp.weixin.qq.com/s?__biz=MzI5NjAwNjg1Nw==&mid=2457137228&idx=1&sn=3f2e42f142c190931c35bebcbd2a2e1b&chksm=fbcab5eaccbd3cfc3dc711234a032d5895dfcb4c97ca5c5a5a723fb1837dc69d9abc68a24893&scene=21#wechat_redirect)
>  * brew install xcodegen
>* [黑幕背后的 Code Signing](https://mp.weixin.qq.com/s?__biz=MzI5NjAwNjg1Nw==&mid=2457137240&idx=1&sn=6bcb062dcc29ecf2473d46387969d7a1&scene=19#wechat_redirect)
>* newpost 
>
```
/Users/devzkn/bin//newpost Code_Signing 摘要、Public-key cryptography、Keychain Access、AppID、Provisioning Profile、entitlements 以及 p12； -t objc
> #原来""的参数，需要自己加上""
```

