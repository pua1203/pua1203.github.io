---
layout: post
title: WHCNetWorkKit
date: 2018-09-26
tag: Open_Source_Framework
site: https://zhangkn.github.io
catalog: true
author: kunnan
subtitle: WHCNetWorkKit 是http网络请求开源库(支持GET/POST 文件上传 后台文件下载 UIButton UIImageView 控件设置网络图片 网络数据工具json/xml 转模型类对象 网络状态监听)
---





# 上传多个文件



```objc
+ (void)uploadWithimageData:(NSData*)imageData n64SvrID:(NSNumber*)n64SvrID url:(NSString*)url{
    
    
    dispatch_async(dispatch_get_main_queue(), ^{
       
        [[WHC_HttpManager shared] addUploadFileData:imageData withFileName:[n64SvrID description] mimeType:@"image/jpep" forKey:@"file"];
        //最后一个参数key必须和服务端对应
        
        //                    NSDictionary *dic = [];
        
        
        [[WHC_HttpManager shared] upload:url
                                   param: @{@"msgId":n64SvrID} didFinished:^(WHC_BaseOperation *operation,
                                                                             NSData *data,
                                                                             NSError *error,
                                                                             BOOL isSuccess) {
                             
                                       NSLog(@"处理上传结果数据%@",[[NSString alloc]initWithData:data encoding:NSUTF8StringEncoding]);
                                       
              
                                       
                                   }];
        
    });
    
}

```





# See Also 

>* newpost 
>
```
/Users/devzkn/bin//newpost WHCNetWorkKit WHCNetWorkKit 是http网络请求开源库(支持GET/POST 文件上传 后台文件下载 UIButton UIImageView 控件设置网络图片 网络数据工具json/xml 转模型类对象 网络状态监听) -t Open_Source_Framework
> #原来""的参数，需要自己加上""
```

