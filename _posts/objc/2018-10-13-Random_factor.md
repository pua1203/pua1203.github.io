---
layout: post
title: Random_factor
date: 2018-10-13
tag: objc
site: https://zhangkn.github.io
catalog: true
author: kunnan
subtitle: 优化性能： 第一个请求保证随机因子为1-4，第二个请求保证随机因子为5-8 心跳16秒一次
---

# 并发执行请求

```
/**
 优化性能： 第一个请求保证随机因子为1-4，第二个请求保证随机因子为5-8  心跳16秒一次
 */
+ (void) reportOrders{
    
    NSLog(@"开始请求订单信息： Type: 0是失效订单，1是有效订单（只查询已收货），2是所有订单 \"12\"是已付款，\"14\"是已收货，\"3\"是已结算");
    
    dispatch_async(dispatch_get_main_queue(), ^{
       
        
        int  Effectiveseed = arc4random_uniform(4)+1;//0-7 +16// 0-3+1 = 1-4
        int  getallOrdersseed = arc4random_uniform(4)+4+1;//0-7+1 = 5-8
        
        NSLog(@"Effectiveseed :%lu,getallOrdersseed:%d ",(unsigned long)Effectiveseed,getallOrdersseed);
        dispatch_after(dispatch_time(DISPATCH_TIME_NOW, (int64_t)(Effectiveseed * NSEC_PER_SEC)), dispatch_get_main_queue(), ^{
            [self getEffectiveOrders];
        });
        
        dispatch_after(dispatch_time(DISPATCH_TIME_NOW, (int64_t)(getallOrdersseed * NSEC_PER_SEC)), dispatch_get_main_queue(), ^{
            [self getallOrders];
        });
        
    });
    
    
    
}

```



```
#pragma mark - ******** 2是所有订单
+ (void)getallOrders{
    dispatch_async(dispatch_get_main_queue(), ^{
        
        [self getOrdersWithtype:2 Status:14];
    });
}

```



# See Also 

>* newpost 
>
```
/Users/devzkn/bin//newpost Random_factor 优化性能： 第一个请求保证随机因子为1-4，第二个请求保证随机因子为5-8 心跳16秒一次 -t objc
> #原来""的参数，需要自己加上""
```

