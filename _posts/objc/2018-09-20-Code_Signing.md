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









#### 具体的操作步骤（你大概扫一下即可，太简单了）













# See Also 

>* newpost 
>
```
/Users/devzkn/bin//newpost Code_Signing 摘要、Public-key cryptography、Keychain Access、AppID、Provisioning Profile、entitlements 以及 p12； -t objc
> #原来""的参数，需要自己加上""
```

