---
layout: post
title: Parsing_URLs_with_regular_expressions
date: 2018-10-12
tag: objc
site: https://zhangkn.github.io
catalog: true
author: kunnan
subtitle: 利用正则表达式解析URL
---



# 用法

```
        NSString *tmpspm =  [KNparseUrlParameter parseUrlParameter:@"spm" urlQueue:tmp.Url];

```



# code 



```
//
//  KNparseUrlParameter.m
//  moonDylib
//
//  Created by devzkn on 10/10/2018.
//  Copyright © 2018 devzkn. All rights reserved.
//

#import "KNparseUrlParameter.h"

@implementation KNparseUrlParameter

//利用正则表达式解析URL
+ (NSString *)parseUrlParameter:(NSString *)key urlQueue:(NSString *)urlQueue
{
    if (!urlQueue || !key) {
        return nil;
    }
    
    NSError *error;
    NSString *regTags=[[NSString alloc] initWithFormat:@"(^|&|\\?)+%@=+([^&]*)(&|$)",key];
    NSRegularExpression *regex = [NSRegularExpression regularExpressionWithPattern:regTags
                                                                           options:NSRegularExpressionCaseInsensitive
                                                                             error:&error];
    
    // 执行匹配的过程
    NSArray *matches = [regex matchesInString:urlQueue
                                      options:0
                                        range:NSMakeRange(0, [urlQueue length])];
    for (NSTextCheckingResult *match in matches) {
        NSString *tagValue = [urlQueue substringWithRange:[match rangeAtIndex:2]];  // 分组2所对应的串
        return tagValue;
    }
    return nil;
}



@end

```



# See Also 

>* newpost 
>
```
/Users/devzkn/bin//newpost Parsing_URLs_with_regular_expressions 利用正则表达式解析URL -t objc
> #原来""的参数，需要自己加上""
```

