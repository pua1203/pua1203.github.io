---
layout: post
title: newWechatInstance
date: 2018-09-29
tag: wx
site: https://zhangkn.github.io
catalog: true
author: kunnan
subtitle: com.tencent.xinWeChat
---

# 前言

/Applications/WeChat.app/Contents/MacOS/WeChat

#### 0x00 传统多开方法



1. `⌘ + N` 大法：适用于 QQ

2. `open -n /Applications/xxx.app` 大法：适用于大部分的应用

3. open /Applications/WeChat.app/Contents/MacOS/WeChat

   * nohup ./WeChat > /dev/null &

     ```
     /Applications/WeChat.app/Contents/MacOS/WeChat ; exit;
     ➜  ~ /Applications/WeChat.app/Contents/MacOS/WeChat ; exit;
     objc[8740]: Class AFHTTPSessionManager is implemented in both /Applications/WeChat.app/Contents/Frameworks/AFNetworking.framework/Versions/A/AFNetworking (0x10a2d2008) and /Applications/WeChat.app/Contents/MacOS/WeChat (0x109a6b528). One of the two will be used. Which one is undefined.
     objc[8740]: Class AFNetworkReachabilityManager is implemented in both /Applications/WeChat.app/Contents/Frameworks/AFNetworking.framework/Versions/A/AFNetworking (0x10a2d1f68) and /Applications/WeChat.app/Contents/MacOS/WeChat (0x109a6b5c8). One of the two will be used. Which one is undefined.
     objc[8740]: Class AFSecurityPolicy is implemented in both /Applications/WeChat.app/Contents/Frameworks/AFNetworking.framework/Versions/A/AFNetworking (0x10a2d1fb8) and /Applications/WeChat.app/Contents/MacOS/WeChat (0x109a6b618). One of the two will be used. Which one is undefined.
     objc[8740]: Class AFQueryStringPair is implemented in both /Applications/WeChat.app/Contents/Frameworks/AFNetworking.framework/Versions/A/AFNetworking (0x10a2d2148) and /Applications/WeChat.app/Contents/MacOS/WeChat (0x109a6b668). One of the two will be used. Which one is undefined.
     objc[8740]: Class AFHTTPRequestSerializer is implemented in both /Applications/WeChat.app/Contents/Frameworks/AFNetworking.framework/Versions/A/AFNetworking (0x10a2d2198) and /Applications/WeChat.app/Contents/MacOS/WeChat (0x109a6b6b8). One of the two will be used. Which one is undefined.
     objc[8740]: Class AFStreamingMultipartFormData is implemented in both /Applications/WeChat.app/Contents/Frameworks/AFNetworking.framework/Versions/A/AFNetworking (0x10a2d21c0) and /Applications/WeChat.app/Contents/MacOS/WeChat (0x109a6b6e0). One of the two will be used. Which one is undefined.
     objc[8740]: Class AFMultipartBodyStream is implemented in both /Applications/WeChat.app/Contents/Frameworks/AFNetworking.framework/Versions/A/AFNetworking (0x10a2d2210) and /Applications/WeChat.app/Contents/MacOS/WeChat (0x109a6b730). One of the two will be used. Which one is undefined.
     objc[8740]: Class AFHTTPBodyPart is implemented in both /Applications/WeChat.app/Contents/Frameworks/AFNetworking.framework/Versions/A/AFNetworking (0x10a2d2238) and /Applications/WeChat.app/Contents/MacOS/WeChat (0x109a6b758). One of the two will be used. Which one is undefined.
     objc[8740]: Class AFJSONRequestSerializer is implemented in both /Applications/WeChat.app/Contents/Frameworks/AFNetworking.framework/Versions/A/AFNetworking (0x10a2d22d8) and /Applications/WeChat.app/Contents/MacOS/WeChat (0x109a6b7f8). One of the two will be used. Which one is undefined.
     objc[8740]: Class AFPropertyListRequestSerializer is implemented in both /Applications/WeChat.app/Contents/Frameworks/AFNetworking.framework/Versions/A/AFNetworking (0x10a2d2328) and /Applications/WeChat.app/Contents/MacOS/WeChat (0x109a6b848). One of the two will be used. Which one is undefined.
     objc[8740]: Class AFHTTPResponseSerializer is implemented in both /Applications/WeChat.app/Contents/Frameworks/AFNetworking.framework/Versions/A/AFNetworking (0x10a2d2378) and /Applications/WeChat.app/Contents/MacOS/WeChat (0x109a6b898). One of the two will be used. Which one is undefined.
     objc[8740]: Class AFJSONResponseSerializer is implemented in both /Applications/WeChat.app/Contents/Frameworks/AFNetworking.framework/Versions/A/AFNetworking (0x10a2d23c8) and /Applications/WeChat.app/Contents/MacOS/WeChat (0x109a6b8e8). One of the two will be used. Which one is undefined.
     objc[8740]: Class AFXMLParserResponseSerializer is implemented in both /Applications/WeChat.app/Contents/Frameworks/AFNetworking.framework/Versions/A/AFNetworking (0x10a2d2418) and /Applications/WeChat.app/Contents/MacOS/WeChat (0x109a6b938). One of the two will be used. Which one is undefined.
     objc[8740]: Class AFXMLDocumentResponseSerializer is implemented in both /Applications/WeChat.app/Contents/Frameworks/AFNetworking.framework/Versions/A/AFNetworking (0x10a2d2468) and /Applications/WeChat.app/Contents/MacOS/WeChat (0x109a6b988). One of the two will be used. Which one is undefined.
     objc[8740]: Class AFPropertyListResponseSerializer is implemented in both /Applications/WeChat.app/Contents/Frameworks/AFNetworking.framework/Versions/A/AFNetworking (0x10a2d24b8) and /Applications/WeChat.app/Contents/MacOS/WeChat (0x109a6b9d8). One of the two will be used. Which one is undefined.
     objc[8740]: Class AFImageResponseSerializer is implemented in both /Applications/WeChat.app/Contents/Frameworks/AFNetworking.framework/Versions/A/AFNetworking (0x10a2d2508) and /Applications/WeChat.app/Contents/MacOS/WeChat (0x109a6ba28). One of the two will be used. Which one is undefined.
     objc[8740]: Class AFCompoundResponseSerializer is implemented in both /Applications/WeChat.app/Contents/Frameworks/AFNetworking.framework/Versions/A/AFNetworking (0x10a2d2558) and /Applications/WeChat.app/Contents/MacOS/WeChat (0x109a6ba78). One of the two will be used. Which one is undefined.
     objc[8740]: Class AFURLSessionManagerTaskDelegate is implemented in both /Applications/WeChat.app/Contents/Frameworks/AFNetworking.framework/Versions/A/AFNetworking (0x10a2d2058) and /Applications/WeChat.app/Contents/MacOS/WeChat (0x109a6bac8). One of the two will be used. Which one is undefined.
     objc[8740]: Class _AFURLSessionTaskSwizzling is implemented in both /Applications/WeChat.app/Contents/Frameworks/AFNetworking.framework/Versions/A/AFNetworking (0x10a2d20d0) and /Applications/WeChat.app/Contents/MacOS/WeChat (0x109a6bb40). One of the two will be used. Which one is undefined.
     objc[8740]: Class AFURLSessionManager is implemented in both /Applications/WeChat.app/Contents/Frameworks/AFNetworking.framework/Versions/A/AFNetworking (0x10a2d20f8) and /Applications/WeChat.app/Contents/MacOS/WeChat (0x109a6bb68). One of the two will be used. Which one is undefined.
     2018-09-29 18:29:03.406 WeChat[8740:572555] Failed to connect (helpButton) outlet from (MMLoginQRCodeViewController) to (NSButton): missing setter or instance variable
     2018-09-29 18:29:03.406 WeChat[8740:572555] Could not connect action, target class MMLoginQRCodeViewController does not respond to -showScanningHelp:
     2018-09-29 18:29:03.446 WeChat[8740:572615] *** -[NSKeyedUnarchiver initForReadingWithData:]: data is NULL
     <CFData 0x7fc29fcb30d0 [0x7fffac9c8570]>{length = 6, capacity = 6, bytes = 0xd0a637ea30f7}
     2018-09-29 18:29:04.169 WeChat[8740:572555] *** -[NSKeyedUnarchiver initForReadingWithData:]: data is NULL
     
     ```






```
Instance is already running!
```





# `if ([CUtility HasWechatInstance] != 0x0) {...}`



![image](https://ws3.sinaimg.cn/large/006tBeITgy1fvql9ibo8oj31fs0jgn29.jpg)







#  swiftOCclass-dump







* **➜**  **/Applications** file /Applications/WeChat.app/Contents/MacOS/WeChat

/Applications/WeChat.app/Contents/MacOS/WeChat: Mach-O 64-bit executable x86_64

*  swiftOCclass-dump  --arch x86_64 /Applications/WeChat.app/Contents/MacOS/WeChat -H -o  /Users/devzkn/decrypted/MacOSWeChat/head  

# See Also 

>* [Mac应用插件](https://github.com/AloneMonkey/MonkeyDev/wiki/Mac%E5%BA%94%E7%94%A8%E6%8F%92%E4%BB%B6)
>  * [get-start-with-mac-reverse](http://www.alonemonkey.com/2017/05/31/get-start-with-mac-reverse/)
>* [一个类似于 Cydia Substrate 的工具，可以用来向 Mac App 注入插件](http://iosre.com/t/macsubstrate-mac-app-ios-cydia-substrate/9802)
>  * 注入到 `launchd` 还要关 `SIP`, 很少有人会选择关 `SIP`.
>  * 还是 `DYLD_INSERT_LIBRARIES` or `inject load_command` 来的方便啊.
>* newpost 
>
```
/Users/devzkn/bin//newpost newWechatInstance com.tencent.xinWeChat -t wx
> #原来""的参数，需要自己加上""
```

