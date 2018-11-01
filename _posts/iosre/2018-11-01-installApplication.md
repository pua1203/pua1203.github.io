---
layout: post
title: installApplication
date: 2018-11-01
tag: iosre
site: https://zhangkn.github.io
catalog: true
author: kunnan
subtitle: 用程序检测更新, 自动下载IPA, 再调那个LSApplicationWorkspace API 进行安装
---



# LSApp



```
    appWorkspace = [LSApplicationWorkspace defaultWorkspace];

    ret = [appWorkspace
                installApplication:[NSURL fileURLWithPath:ipaPath]
                withOptions:nil
                error:error
                usingBlock:^(id obj, void *unknow) {
                }
            ];

```





# See Also 

>* newpost 
>
```
/Users/devzkn/bin//newpost installApplication 用程序检测更新, 自动下载IPA, 再调那个LSApplicationWorkspace API 进行安装 -t iosre
> #原来""的参数，需要自己加上""
```

