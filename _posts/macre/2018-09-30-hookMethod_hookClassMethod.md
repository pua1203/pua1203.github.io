---
layout: post
title: hookMethod_hookClassMethod
date: 2018-09-30
tag: macre
site: https://zhangkn.github.io
catalog: true
author: kunnan
subtitle: 利用runtime或者substrate 进行hook
---





# I 、kn_hookMethod、kn_hookClassMethod

利用`runtime.h` 进行hook

#### code

```
/**
 替换对象方法
 
 @param originalClass 原始类
 @param originalSelector 原始类的方法
 @param swizzledClass 替换类
 @param swizzledSelector 替换类的方法
 */

void kn_hookMethod(Class originalClass, SEL originalSelector, Class swizzledClass, SEL swizzledSelector){
    
    Method originalMethod = class_getInstanceMethod(originalClass, originalSelector);
    Method swizzledMethod = class_getInstanceMethod(swizzledClass, swizzledSelector);
    if(originalMethod && swizzledMethod) {
        method_exchangeImplementations(originalMethod, swizzledMethod);
    }

    
}


/**
 替换类方法
 
 @param originalClass 原始类
 @param originalSelector 原始类的类方法
 @param swizzledClass 替换类
 @param swizzledSelector 替换类的类方法
 */


void kn_hookClassMethod(Class originalClass, SEL originalSelector, Class swizzledClass, SEL swizzledSelector){
    Method originalMethod = class_getClassMethod(originalClass, originalSelector);
    Method swizzledMethod = class_getClassMethod(swizzledClass, swizzledSelector);
    if(originalMethod && swizzledMethod) {
        method_exchangeImplementations(originalMethod, swizzledMethod);
    }

}

12345678910111213141516171819202122232425262728293031323334353637383940
```

#### demo

```
static void __attribute__((constructor)) initialize(void) {
    MSHookMessageEx(objc_getClass("MessageService"),  @selector(OnSyncBatchAddMsgs:isFirstSync:), (IMP)&new_MessageService_OnSyncBatchAddMsgs_isFirstSync, (IMP*)&origin_new_MessageService_OnSyncBatchAddMsgs_isFirstSync);
    
    [NSObject hookWeChat];
}

123456
#import "NSObject+WeChatHook.h"

@implementation NSObject (WeChatHook)


+ (void)hookWeChat {    
    
    kn_hookClassMethod(objc_getClass("CUtility"), @selector(HasWechatInstance), [self class], @selector(hook_HasWechatInstance));   
}
#pragma mark - hook 方法
/**
 hook 是否已启动
 */
+ (BOOL)hook_HasWechatInstance {
    NSLog(@"kn hook_HasWechatInstance");
    return NO;
}
@end
123456789101112131415161718
```

# II 、使用`substrate.h` 进行hook

```
static void (*origin_new_MessageService_OnSyncBatchAddMsgs_isFirstSync)(MessageService*,SEL,NSArray *,BOOL);
static void new_MessageService_OnSyncBatchAddMsgs_isFirstSync(MessageService* self,SEL _cmd,NSArray * msgs,BOOL isFirstSync){
    origin_new_MessageService_OnSyncBatchAddMsgs_isFirstSync(self,_cmd,msgs,isFirstSync);
}
```

  ---------------------  本文来自 iOS&macOS 应用逆向与安全 的CSDN 博客 ，全文地址请点击：https://blog.csdn.net/z929118967/article/details/78216856?utm_source=copy 

# See Also 

>* newpost 
>
```
/Users/devzkn/bin//newpost hookMethod_hookClassMethod 利用runtime或者substrate 进行hook -t macre
> #原来""的参数，需要自己加上""
```

