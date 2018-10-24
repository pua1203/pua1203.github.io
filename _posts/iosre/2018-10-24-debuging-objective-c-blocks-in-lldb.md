---
layout: post
title: debuging-objective-c-blocks-in-lldb
date: 2018-10-24
tag: iosre
site: https://zhangkn.github.io
catalog: true
author: kunnan
subtitle: 通过block的方法签名获取 Block 到底有几个参数
---



# 前言



* 在 LLVM 文档中，可以看到 [Block 的实现规范 49](http://clang.llvm.org/docs/Block-ABI-Apple.html)，其中最关键的地方是对于 Block 内存结构的定义：

  ```objc
  struct Block_literal_1 {
      void *isa; // initialized to &_NSConcreteStackBlock or &_NSConcreteGlobalBlock
      int flags;
      int reserved;
      void (*invoke)(void *, ...);
      struct Block_descriptor_1 {
      	unsigned long int reserved;         // NULL
          unsigned long int size;         // sizeof(struct Block_literal_1)
          // optional helper functions
          void (*copy_helper)(void *dst, void *src);     // IFF (1<<25)
          void (*dispose_helper)(void *src);             // IFF (1<<25)
          // required ABI.2010.3.16
          const char *signature;                         // IFF (1<<30)
      } *descriptor;
      // imported variables
  };
  
  ```

重点要关注的就是 `void (*invode)(void *, ...);` 和 descriptor 中的 `const char *signature`，前者指向了 Block 具体实现的地址，后者是表示 Block 函数签名的字符串。





* Forwarding local port 1234 to remote port 1234

* `po $x4`

  ```
  <__NSStackBlock__: 0x16fd88f88>
  
  ```

* 在 64 位系统上，指针类型的大小是 8 个字节，而 int 是 4 个字节，如下：

  * ```
    (lldb) memory read --size 8 --format x 0x16fd88f88
    0x16fd88f88: 0x000000019b4d8088 0x00000000c2000000
    0x16fd88f98: 0x00000001000dd770 0x0000000100fc6610
    0x16fd88fa8: 0x000000017444c510 0x0000000000000001
    0x16fd88fb8: 0x000000017444c510 0x0000000000000008
    
    ```

  * 反汇编(函数指针的地址是在第 16 个字节之后，并占用 8 个字节，所以可以得到函数的地址是 0x00000001000dd770。)

    * (lldb) disassemble --start-address 0x00000001000dd770

* 找出 Block 的函数签名

  * 要找出 Block 的函数签名，需要通过 `descriptor` 结构体中的 `signature` 成员，然后通过它得到一个 `NSMethodSignature` 对象。

  * 首先，需要找到 `descriptor` 结构体。这个结构体在 Block 中是通过指针持有的，它的位置正好在 `invoke` 成员后面，占用 8 个字节。可以从上面的内存打印中看到 `descriptor` 指针的地址是 **0x0000000100fc6610**。

  * `signature` 的地址是在 `descriptor` 下偏移两个 unsiged long 和两个指针后的地址，即 32 个字节后。现在让我们找出它的地址，并打印出它的字符串内容：

  * ```
    (lldb) memory read --size 8 --format x 0x0000000100fc6610
    0x100fc6610: 0x0000000000000000 0x0000000000000029
    0x100fc6620: 0x00000001000ddb64 0x00000001000ddb70
    0x100fc6630: 0x0000000100dfec18 0x0000000000000001
    0x100fc6640: 0x0000000000000000 0x0000000000000048
    
    (lldb) p (char *)0x0000000100dfec18
    (char *) $4 = 0x0000000100dfec18 "v28@?0q8@"NSDictionary"16B24"
    
    ```

  *  `NSMethodSignature` 找出它的参数类型：

    ```
    (lldb) po [NSMethodSignature signatureWithObjCTypes:"v28@?0q8@\"NSDictionary\"16B24"]
    <NSMethodSignature: 0x174672940>
        number of arguments = 4
        frame size = 224
        is special struct return? NO
        return value: -------- -------- -------- --------
            type encoding (v) 'v'
            flags {}
            modifiers {}
            frame {offset = 0, offset adjust = 0, size = 0, size adjust = 0}
            memory {offset = 0, size = 0}
        argument 0: -------- -------- -------- --------
            type encoding (@) '@?'
            flags {isObject, isBlock}
            modifiers {}
            frame {offset = 0, offset adjust = 0, size = 8, size adjust = 0}
            memory {offset = 0, size = 8}
        argument 1: -------- -------- -------- --------
            type encoding (q) 'q'
            flags {isSigned}
            modifiers {}
            frame {offset = 8, offset adjust = 0, size = 8, size adjust = 0}
            memory {offset = 0, size = 8}
        argument 2: -------- -------- -------- --------
            type encoding (@) '@"NSDictionary"'
            flags {isObject}
            modifiers {}
            frame {offset = 16, offset adjust = 0, size = 8, size adjust = 0}
            memory {offset = 0, size = 8}
                class 'NSDictionary'
        argument 3: -------- -------- -------- --------
            type encoding (B) 'B'
            flags {}
            modifiers {}
            frame {offset = 24, offset adjust = 0, size = 8, size adjust = -7}
            memory {offset = 0, size = 1}
    
    ```


  #### other : 通过 flags 与 block 中定义的枚举掩码进行与判断

  ```
  enum {
      BLOCK_HAS_COPY_DISPOSE =  (1 << 25),
      BLOCK_HAS_CTOR =          (1 << 26), // helpers have C++ code
      BLOCK_IS_GLOBAL =         (1 << 28),
      BLOCK_HAS_STRET =         (1 << 29), // IFF BLOCK_HAS_SIGNATURE
      BLOCK_HAS_SIGNATURE =     (1 << 30),
  };
  
  ```

  * image list -o -f |grep dylb

    ```
    (lldb) image list -o -f 
    [  0] 0x0000000000074000 /private/var/mobile/Containers/Bundle/Application/D106C0E3-D874-4534-AED6-A7104131B31D/LuoJiFM-IOS.app/LuoJiFM-IOS(0x0000000100074000)
    [  1] 0x000000000002c000 /Users/wordbeyond/Library/Developer/Xcode/iOS DeviceSupport/8.2 (12D508)/Symbols/usr/lib/dyld
    
    ```

  * 由于 `((0xc2000000 & (1 << 30)) != 0)`，因此我们可以确定这个 Block 是有签名的。

    >

# See Also 



#### iosre



* http://iosre.com/t/nsmallocblock/11448/2

* [善用搜索 ](http://iosre.com/t/when-you-come-across---nsxxxblock---0xrandomnumber-while-debugging-a-block-in-lldb-how-to-locate-the-block/4977)

  ```
  (lldb) po $x5
  <__NSStackBlock__: 0x16fd26ac8>
  
  (lldb) memory read --size 8 --format x 0x16fd26ac8
  0x16fd26ac8: 0x00000001a0d11558 0x00000000c2000000
  0x16fd26ad8: 0x00000001022d4638 0x00000001037ab4f0
  0x16fd26ae8: 0x0000000126f4a1c0 0x0000000126ac9ae0
  0x16fd26af8: 0x00000001821e7f00 0x0000000124d31400
  Note, for arm64, the 2nd command is memory read --size 8, while for armv7/armv7s it should be memory read --size 4.
  
  The value you get from 0x00000001022d4638 - ASLR offset is the address of the block. Go to this address in IDA or hopper then you’ll see the block implementation.
  
  
  ```




>* http://www.swiftyper.com/2016/12/16/debuging-objective-c-blocks-in-lldb/
>* http://iosre.com/t/block/6779
>* newpost 
>
```
/Users/devzkn/bin//newpost debuging-objective-c-blocks-in-lldb 通过block的方法签名获取 Block 到底有几个参数 -t iosre
> #原来""的参数，需要自己加上""
```

