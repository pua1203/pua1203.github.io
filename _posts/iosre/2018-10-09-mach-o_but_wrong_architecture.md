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

* [VI 架构不匹配的时候报：`mach-o, but wrong architecture`](https://kunnan.github.io/2018/07/01/dumpdecrypted/#vi-%E6%9E%B6%E6%9E%84%E4%B8%8D%E5%8C%B9%E9%85%8D%E7%9A%84%E6%97%B6%E5%80%99%E6%8A%A5mach-o-but-wrong-architecture)



# See Also 

>* https://kunnan.github.io/2018/07/01/dumpdecrypted/
>* https://zhangkn.github.io/2017/12/frida/
>* newpost 
>
```
/Users/devzkn/bin//newpost mach-o_but_wrong_architecture 解决 dumpdecrypted 之后的架构不匹配的问题 -t iosre
> #原来""的参数，需要自己加上""
```

