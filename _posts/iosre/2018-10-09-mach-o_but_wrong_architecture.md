---
layout: post
title: mach-o_but_wrong_architecture
date: 2018-10-09
tag: iosre
site: https://zhangkn.github.io
catalog: true
author: kunnan
subtitle: 解决 dumpdecrypted 之后的架构不匹配的问题
---



#  前言



```
dyld: Library not loaded: @rpath/libswiftAVFoundation.dylib
  Referenced from: /private/var/mobile/Containers/Bundle/Application/CD2B7906-AD07-40EA-B2B9-6C934B84D9D5/moon.app/Moon
  Reason: no suitable image found.  Did find:
  /private/var/mobile/Containers/Bundle/Application/CD2B7906-AD07-40EA-B2B9-6C934B84D9D5/moon.app/Frameworks/libswiftAVFoundation.dylib: mach-o, but wrong architecture
```

* ls -lrt Frameworks

  ```
  ➜  Frameworks ls -lrt
  total 15000
  -rw-r-xr-x  1 devzkn  staff    65872 Oct  9 14:33 libswiftContacts.dylib
  -rw-r-xr-x  1 devzkn  staff   126144 Oct  9 14:33 libswiftAVFoundation.dylib
  -rw-r-xr-x  1 devzkn  staff   333152 Oct  9 14:33 libswiftsimd.dylib
  -rw-r-xr-x  1 devzkn  staff    66656 Oct  9 14:33 libswiftos.dylib
  -rw-r-xr-x  1 devzkn  staff   109872 Oct  9 14:33 libswiftUIKit.dylib
  -rw-r-xr-x  1 devzkn  staff    63536 Oct  9 14:33 libswiftQuartzCore.dylib
  -rw-r-xr-x  1 devzkn  staff    64000 Oct  9 14:33 libswiftPhotos.dylib
  -rw-r-xr-x  1 devzkn  staff    67328 Oct  9 14:33 libswiftObjectiveC.dylib
  -rw-r-xr-x  1 devzkn  staff    66160 Oct  9 14:33 libswiftMetal.dylib
  -rw-r-xr-x  1 devzkn  staff  1794640 Oct  9 14:33 libswiftFoundation.dylib
  -rw-r-xr-x  1 devzkn  staff   188992 Oct  9 14:33 libswiftDispatch.dylib
  -rw-r-xr-x  1 devzkn  staff    95936 Oct  9 14:33 libswiftDarwin.dylib
  -rw-r-xr-x  1 devzkn  staff    66208 Oct  9 14:33 libswiftCoreMedia.dylib
  -rw-r-xr-x  1 devzkn  staff    66496 Oct  9 14:33 libswiftCoreLocation.dylib
  -rw-r-xr-x  1 devzkn  staff    62432 Oct  9 14:33 libswiftCoreImage.dylib
  -rw-r-xr-x  1 devzkn  staff   141776 Oct  9 14:33 libswiftCoreGraphics.dylib
  -rw-r-xr-x  1 devzkn  staff    61568 Oct  9 14:33 libswiftCoreFoundation.dylib
  -rw-r-xr-x  1 devzkn  staff    76800 Oct  9 14:33 libswiftCoreData.dylib
  -rw-r-xr-x  1 devzkn  staff    65728 Oct  9 14:33 libswiftCoreAudio.dylib
  -rw-r-xr-x  1 devzkn  staff  4045984 Oct  9 14:33 libswiftCore.dylib
  drwxr-xr-x  6 devzkn  staff      192 Oct  9 14:43 UNWShareKit.framework
  
  ```


# I、先dumpdecrypted



#### `Forwarding local port 2222 to remote port 22`

* **➜**  **pua1203.github.io** **git:(****master****)** port22

  ```
  Forwarding local port 2222 to remote port 22
  
  Incoming connection to 2222
  
  Waiting for devices...
  
  Connecting to device <MuxDevice: ID 1 ProdID 0x12a8 Serial '07cf5424d3844522c3396fc55f419a11633cb54c' Location 0x14200000>
  
  Connection established, relaying data
  
  
  
  ```


####   [frida-ios-dump](https://github.com/AloneMonkey/frida-ios-dump) 



必须确保Mac的版本和手机端的Frida版本保持一致。



否则报`**Failed to enumerate processes: unable to communicate with remote frida-server; please ensure that major versions match and that the remote Frida has the feature you are trying to use**`





*  frida-ps -Ua

  ```
  PID  Name       Identifier          
  ---  ---------  --------------------
  954  App Store  com.apple.AppStore  
  887  Cydia      com.saurik.Cydia    
  885  微信         com.tencent.xin     
  996  淘宝联盟       com.alimama.moon    
  883  邮件         com.apple.mobilemail
  
  ```




* [knpydump](https://github.com/zhangkn/KNBin/blob/master/knpydump)

  * **➜**  **bin** **git:(****master****)** knpydump com.alimama.moon

  * 0.00B [00:00, ?B/s]Generating "淘宝联盟.ipa"

    ```
    Dumping 淘宝联盟 to /var/folders/8s/t119mw8d4lsdztx8h9q8113m0000gn/T
    start dump /private/var/mobile/Containers/Bundle/Application/E9E01F17-6505-4033-8793-2E950B778B2B/Moon.app/Moon
    Moon.fid: 100%|█████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████| 11.9M/11.9M [00:01<00:00, 8.48MB/s]
    start dump /private/var/mobile/Containers/Bundle/Application/E9E01F17-6505-4033-8793-2E950B778B2B/Moon.app/Frameworks/UNWShareKit.framework/UNWShareKit
    UNWShareKit.fid: 100%|████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████| 689k/689k [00:00<00:00, 5.89MB/s]
    start dump /private/var/mobile/Containers/Bundle/Application/E9E01F17-6505-4033-8793-2E950B778B2B/Moon.app/Frameworks/libswiftAVFoundation.dylib
    libswiftAVFoundation.dylib.fid: 100%|█████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████| 123k/123k [00:00<00:00, 1.04MB/s]
    start dump /private/var/mobile/Containers/Bundle/Application/E9E01F17-6505-4033-8793-2E950B778B2B/Moon.app/Frameworks/libswiftContacts.dylib
    libswiftContacts.dylib.fid: 100%|████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████| 64.1k/64.1k [00:00<00:00, 926kB/s]
    start dump /private/var/mobile/Containers/Bundle/Application/E9E01F17-6505-4033-8793-2E950B778B2B/Moon.app/Frameworks/libswiftCore.dylib
    libswiftCore.dylib.fid: 100%|███████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████| 4.22M/4.22M [00:00<00:00, 10.3MB/s]
    start dump /private/var/mobile/Containers/Bundle/Application/E9E01F17-6505-4033-8793-2E950B778B2B/Moon.app/Frameworks/libswiftCoreAudio.dylib
    libswiftCoreAudio.dylib.fid: 100%|███████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████| 80.6k/80.6k [00:00<00:00, 699kB/s]
    start dump /private/var/mobile/Containers/Bundle/Application/E9E01F17-6505-4033-8793-2E950B778B2B/Moon.app/Frameworks/libswiftCoreFoundation.dylib
    libswiftCoreFoundation.dylib.fid: 100%|██████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████| 60.1k/60.1k [00:00<00:00, 841kB/s]
    start dump /private/var/mobile/Containers/Bundle/Application/E9E01F17-6505-4033-8793-2E950B778B2B/Moon.app/Frameworks/libswiftCoreGraphics.dylib
    libswiftCoreGraphics.dylib.fid: 100%|█████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████| 138k/138k [00:00<00:00, 1.20MB/s]
    start dump /private/var/mobile/Containers/Bundle/Application/E9E01F17-6505-4033-8793-2E950B778B2B/Moon.app/Frameworks/libswiftCoreImage.dylib
    libswiftCoreImage.dylib.fid: 100%|███████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████| 60.9k/60.9k [00:00<00:00, 853kB/s]
    start dump /private/var/mobile/Containers/Bundle/Application/E9E01F17-6505-4033-8793-2E950B778B2B/Moon.app/Frameworks/libswiftCoreLocation.dylib
    libswiftCoreLocation.dylib.fid: 100%|████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████| 64.7k/64.7k [00:00<00:00, 524kB/s]
    start dump /private/var/mobile/Containers/Bundle/Application/E9E01F17-6505-4033-8793-2E950B778B2B/Moon.app/Frameworks/libswiftCoreMedia.dylib
    libswiftCoreMedia.dylib.fid: 100%|███████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████| 64.5k/64.5k [00:00<00:00, 537kB/s]
    start dump /private/var/mobile/Containers/Bundle/Application/E9E01F17-6505-4033-8793-2E950B778B2B/Moon.app/Frameworks/libswiftDarwin.dylib
    libswiftDarwin.dylib.fid: 100%|██████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████| 93.5k/93.5k [00:00<00:00, 814kB/s]
    start dump /private/var/mobile/Containers/Bundle/Application/E9E01F17-6505-4033-8793-2E950B778B2B/Moon.app/Frameworks/libswiftDispatch.dylib
    libswiftDispatch.dylib.fid: 100%|█████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████| 202k/202k [00:00<00:00, 1.72MB/s]
    start dump /private/var/mobile/Containers/Bundle/Application/E9E01F17-6505-4033-8793-2E950B778B2B/Moon.app/Frameworks/libswiftFoundation.dylib
    libswiftFoundation.dylib.fid: 100%|█████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████| 1.89M/1.89M [00:00<00:00, 8.82MB/s]
    start dump /private/var/mobile/Containers/Bundle/Application/E9E01F17-6505-4033-8793-2E950B778B2B/Moon.app/Frameworks/libswiftMetal.dylib
    libswiftMetal.dylib.fid: 100%|███████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████| 64.5k/64.5k [00:00<00:00, 556kB/s]
    start dump /private/var/mobile/Containers/Bundle/Application/E9E01F17-6505-4033-8793-2E950B778B2B/Moon.app/Frameworks/libswiftObjectiveC.dylib
    libswiftObjectiveC.dylib.fid: 100%|██████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████| 65.8k/65.8k [00:00<00:00, 568kB/s]
    start dump /private/var/mobile/Containers/Bundle/Application/E9E01F17-6505-4033-8793-2E950B778B2B/Moon.app/Frameworks/libswiftPhotos.dylib
    libswiftPhotos.dylib.fid: 100%|██████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████| 62.3k/62.3k [00:00<00:00, 512kB/s]
    start dump /private/var/mobile/Containers/Bundle/Application/E9E01F17-6505-4033-8793-2E950B778B2B/Moon.app/Frameworks/libswiftQuartzCore.dylib
    libswiftQuartzCore.dylib.fid: 100%|██████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████| 61.8k/61.8k [00:00<00:00, 520kB/s]
    start dump /private/var/mobile/Containers/Bundle/Application/E9E01F17-6505-4033-8793-2E950B778B2B/Moon.app/Frameworks/libswiftUIKit.dylib
    libswiftUIKit.dylib.fid: 100%|█████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████| 107k/107k [00:00<00:00, 871kB/s]
    start dump /private/var/mobile/Containers/Bundle/Application/E9E01F17-6505-4033-8793-2E950B778B2B/Moon.app/Frameworks/libswiftsimd.dylib
    libswiftsimd.dylib.fid: 100%|█████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████| 426k/426k [00:00<00:00, 3.59MB/s]
    start dump /private/var/mobile/Containers/Bundle/Application/E9E01F17-6505-4033-8793-2E950B778B2B/Moon.app/Frameworks/libswiftos.dylib
    libswiftos.dylib.fid: 100%|██████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████| 65.1k/65.1k [00:00<00:00, 532kB/s]
    start dump /private/var/mobile/Containers/Bundle/Application/E9E01F17-6505-4033-8793-2E950B778B2B/Moon.app/Frameworks/libswiftCoreData.dylib
    libswiftCoreData.dylib.fid: 100%|████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████████| 74.7k/74.7k [00:00<00:00, 627kB/s]
    Localizable.strings: 66.1MB [00:07, 489kB/s]                                                                                                                                                                         
    
    ```


  # [ 架构不匹配的时候报：`mach-o, but wrong architecture`](https://kunnan.github.io/2018/07/01/dumpdecrypted/#vi-%E6%9E%B6%E6%9E%84%E4%B8%8D%E5%8C%B9%E9%85%8D%E7%9A%84%E6%97%B6%E5%80%99%E6%8A%A5mach-o-but-wrong-architecture)

#### file Moon : 查看架构

* **➜**  **bin** **git:(****master****)** cd /Users/devzkn/decrypted/com.alimama.moon/5.6.1/Payload/Moon.app 

  **➜**  **Moon.app** file Moon

  Moon: Mach-O executable arm_v7

此时需要使用arm64 机器进行获取新的的ipa 包。然后进行合并。



#### 系统库就不用合并了：





```
start dump /private/var/mobile/Containers/Bundle/Application/E9E01F17-6505-4033-8793-2E950B778B2B/Moon.app/Frameworks/libswiftCore.dylib

```

* 因此只要合并以下两个二进制文件
  * `start dump /private/var/mobile/Containers/Bundle/Application/E9E01F17-6505-4033-8793-2E950B778B2B/Moon.app/Frameworks/UNWShareKit.framework/UNWShareKit`
  * `start dump /private/var/mobile/Containers/Bundle/Application/E9E01F17-6505-4033-8793-2E950B778B2B/Moon.app/Moon`



# lipo (建议使用脚本lipo)

* 更新ipa 之后，记得一起删除掉.app

![image](https://wx4.sinaimg.cn/large/006tBeITgy1fw21glavi8j30b2052jrk.jpg)

* **➜**  **Moon.app** lipo -create ./Moon /Users/devzkn/decrypted/com.alimama.moon/5.6.1/arm_v7Payload/Moon.app/Moon -output ./Moon

  ```
  ➜  Moon.app file Moon
  Moon: Mach-O universal binary with 2 architectures: [arm_v7] [arm64:Mach-O 64-bit executable arm64]
  Moon (for architecture armv7):	Mach-O executable arm_v7
  Moon (for architecture arm64):	Mach-O 64-bit executable arm64
  
  ```


* /Users/devzkn/decrypted/com.alimama.moon/5.6.1/Payload/Moon.app/Frameworks/UNWShareKit.framework

  ```
  lipo -create ./UNWShareKit  /Users/devzkn/decrypted/com.alimama.moon/5.6.1/arm_v7Payload/Moon.app/Frameworks/UNWShareKit.framework/UNWShareKit -output  ./UNWShareKit
  ```


* libswiftAVFoundation.dylib

  ```
  ➜  Frameworks lipo -create ./libswiftAVFoundation.dylib /Users/devzkn/decrypted/com.alimama.moon/5.6.1/arm_v7Payload/Moon.app/Frameworks/libswiftAVFoundation.dylib  -output  ./libswiftAVFoundation.dylib 
  
  ```

* **libswiftContacts.dylib**

  ```
  lipo -create ./libswiftContacts.dylib /Users/devzkn/decrypted/com.alimama.moon/5.6.1/arm_v7Payload/Moon.app/Frameworks/libswiftContacts.dylib  -output  ./libswiftContacts.dylib
  
  ```


* libswiftCore.dylib

  ```
  ➜  Frameworks lipo -create ./libswiftCore.dylib /Users/devzkn/decrypted/com.alimama.moon/5.6.1/arm_v7Payload/Moon.app/Frameworks/libswiftCore.dylib  -output  ./libswiftCore.dylib 
  
  ```


* libswiftCoreAudio.dylib 

  ```
  lipo -create ./libswiftCoreAudio.dylib /Users/devzkn/decrypted/com.alimama.moon/5.6.1/arm_v7Payload/Moon.app/Frameworks/libswiftCoreAudio.dylib  -output  ./libswiftCoreAudio.dylib
  
  ```

* libswiftCoreFoundation.dylib

  ```
  lipo -create ./libswiftCoreFoundation.dylib /Users/devzkn/decrypted/com.alimama.moon/5.6.1/arm_v7Payload/Moon.app/Frameworks/libswiftCoreFoundation.dylib  -output  ./libswiftCoreFoundation.dylib
  
  ```


* libswiftCoreGraphics.dylib

  ```
  lipo -create ./libswiftCoreGraphics.dylib /Users/devzkn/decrypted/com.alimama.moon/5.6.1/arm_v7Payload/Moon.app/Frameworks/libswiftCoreGraphics.dylib  -output  ./libswiftCoreGraphics.dylib
  
  ```


* libswiftCoreImage.dylib

  ```
  lipo -create ./libswiftCoreImage.dylib /Users/devzkn/decrypted/com.alimama.moon/5.6.1/arm_v7Payload/Moon.app/Frameworks/libswiftCoreImage.dylib  -output  ./libswiftCoreImage.dylib
  ```


* libswiftCoreLocation.dylib

  ```
  lipo -create ./libswiftCoreLocation.dylib /Users/devzkn/decrypted/com.alimama.moon/5.6.1/arm_v7Payload/Moon.app/Frameworks/libswiftCoreLocation.dylib  -output  ./libswiftCoreLocation.dylib
  ```


* libswiftCoreMedia.dylib 

  ```
  lipo -create ./libswiftCoreMedia.dylib /Users/devzkn/decrypted/com.alimama.moon/5.6.1/arm_v7Payload/Moon.app/Frameworks/libswiftCoreMedia.dylib  -output  ./libswiftCoreMedia.dylib
  
  ```


* libswiftDarwin.dylib 

  ```
  lipo -create ./libswiftDarwin.dylib /Users/devzkn/decrypted/com.alimama.moon/5.6.1/arm_v7Payload/Moon.app/Frameworks/libswiftDarwin.dylib  -output  ./libswiftDarwin.dylib
  
  ```


* libswiftDispatch.dylib

  ```
  lipo -create ./libswiftDispatch.dylib /Users/devzkn/decrypted/com.alimama.moon/5.6.1/arm_v7Payload/Moon.app/Frameworks/libswiftDispatch.dylib  -output  ./libswiftDispatch.dylib
  
  ```


* libswiftFoundation.dylib

  ```
  lipo -create ./libswiftFoundation.dylib /Users/devzkn/decrypted/com.alimama.moon/5.6.1/arm_v7Payload/Moon.app/Frameworks/libswiftFoundation.dylib  -output  ./libswiftFoundation.dylib
  
  ```


* libswiftMetal.dylib

  ```
  lipo -create ./libswiftMetal.dylib /Users/devzkn/decrypted/com.alimama.moon/5.6.1/arm_v7Payload/Moon.app/Frameworks/libswiftMetal.dylib  -output  ./libswiftMetal.dylib
  
  ```


* libswiftObjectiveC.dylib

  ```
  lipo -create ./libswiftObjectiveC.dylib /Users/devzkn/decrypted/com.alimama.moon/5.6.1/arm_v7Payload/Moon.app/Frameworks/libswiftObjectiveC.dylib  -output  ./libswiftObjectiveC.dylib
  
  ```

* libswiftPhotos.dylib

  ```
  lipo -create ./libswiftPhotos.dylib /Users/devzkn/decrypted/com.alimama.moon/5.6.1/arm_v7Payload/Moon.app/Frameworks/libswiftPhotos.dylib  -output  ./libswiftPhotos.dylib
  
  ```


* **libswiftQuartzCore.dylib**

  ```
  lipo -create ./libswiftQuartzCore.dylib /Users/devzkn/decrypted/com.alimama.moon/5.6.1/arm_v7Payload/Moon.app/Frameworks/libswiftQuartzCore.dylib  -output  ./libswiftQuartzCore.dylib
  
  ```


* **libswiftUIKit.dylib**

  ```
  ➜  Frameworks lipo -create ./libswiftUIKit.dylib /Users/devzkn/decrypted/com.alimama.moon/5.6.1/arm_v7Payload/Moon.app/Frameworks/libswiftUIKit.dylib  -output  ./libswiftUIKit.dylib
  
  ```

* **libswiftsimd.dylib**

  ```
  lipo -create ./libswiftsimd.dylib /Users/devzkn/decrypted/com.alimama.moon/5.6.1/arm_v7Payload/Moon.app/Frameworks/libswiftsimd.dylib  -output  ./libswiftsimd.dylib
  
  ```


* libswiftos.dylib

  ```
  lipo -create ./libswiftos.dylib /Users/devzkn/decrypted/com.alimama.moon/5.6.1/arm_v7Payload/Moon.app/Frameworks/libswiftos.dylib  -output  ./libswiftos.dylib
  
  ```


* **libswiftCoreData.dylib**

  ```
  lipo -create ./libswiftCoreData.dylib /Users/devzkn/decrypted/com.alimama.moon/5.6.1/arm_v7Payload/Moon.app/Frameworks/libswiftCoreData.dylib  -output  ./libswiftCoreData.dylib
  ```


# See Also 

![image](https://wx4.sinaimg.cn/large/006tBeITgy1fw23ayjxeoj31a40le11x.jpg)

# other 



* 以arm64 为基础进行合并的时候，发现手机没有以下动态库，因此需要合并。

  ```
  dyld: Library not loaded: @rpath/libswiftAVFoundation.dylib
    Referenced from: /private/var/mobile/Containers/Bundle/Application/CD2B7906-AD07-40EA-B2B9-6C934B84D9D5/moon.app/Moon
    Reason: no suitable image found.  Did find:
  	/private/var/mobile/Containers/Bundle/Application/CD2B7906-AD07-40EA-B2B9-6C934B84D9D5/moon.app/Frameworks/libswiftAVFoundation.dylib: mach-o, but wrong architecture
  	/private/var/mobile/Containers/Bundle/Application/CD2B7906-AD07-40EA-B2B9-6C934B84D9D5/moon.app/Frameworks/libswiftAVFoundation.dylib: mach-o, but wrong architecture
  	/private/var/mobile/Containers/Bundle/Application/CD2B7906-AD07-40EA-B2B9-6C934B84D9D5/moon.app/Frameworks/libswiftAVFoundation.dylib: mach-o, but wrong architecture
  ```




>* https://kunnan.github.io/2018/07/01/dumpdecrypted/
>
>* https://zhangkn.github.io/2017/12/frida/
>
>* newpost 
>
>* # [Objective-C混淆之方法名混淆](https://www.jianshu.com/p/3a8fb6f7c55f)
>
>  * https://github.com/tom555cat/obfuscator-clang
>  * http://iosre.com/t/clang-objective-c/13163
>  * [ClangAutoStats.cpp](https://github.com/zhangkn/obfuscator-clang/blob/master/ClangAutoStats.cpp)
>
```
/Users/devzkn/bin//newpost mach-o_but_wrong_architecture 解决 dumpdecrypted 之后的架构不匹配的问题 -t iosre
> #原来""的参数，需要自己加上""
```

