---
layout: post
title: Why_the_IT_industry_is_progressing_so_fast
date: 2018-11-15
tag: GoogleMethodology
site: https://zhangkn.github.io
catalog: true
author: kunnan
subtitle: IT行业为什么进步这么快?阿姆达尔法则（Amdahl Law）这是IT行业得以快速进步的战术，和它相对应的是摩尔定律，这是IT行业的战略。
---







# 前言



阿姆达尔在设计计算机系统时，充分认识到了计算机各部分的性能必须平衡匹配，才能得到整体性能最佳的系统。他将这种思想用一个简单的公式描述出来：

![image](https://wx4.sinaimg.cn/large/af39b376gy1fx8u7hykrfj20mg062dg8.jpg)





* 在公式左边的大写的S代表系统最后的性能提升（加速），

* 右边分母中的小写的s，代表某一项指标的性能提升，比如你把计算机里面内存的速度提升了两倍，右边的小s就是两倍。

* p代表这项提升被用到的比例（或者说概率，因为在计算机中一个局部对计算时间的影响是估计出来的，因此阿姆达尔用概率p代表），比如说内存的读写访问，占了计算机程序运行的20%的时间。





如果你把内存的速度翻一番，即s＝2，那么整个计算机性能的提升是多少呢？根据这个公式，可以算出是11%。这个结果看起来还是不错的，如果你有办法将内存的速度提升到原来的100倍，那么计算机整体速度只能提升约25%，这看上去就不大有效了。



# 例子



1、假如内存读写占用程序运行时间的20%，处理器运算占60%。今天有两个技术，一个可以将内存读写速度提高5倍，另一个可以将处理器的速度提升50%，由于成本的限制和研发时间的限制，下一个版本只能采用一项改进。你应该选用哪个？

很多人会想，20%的5倍，好像效果显著；而60%的50%，也就30%，所以当然应该采用新的内存技术。阿姆达尔法则给出的结论，则恰恰相反。根据上述公式，提高内存的性能，计算机整体的性能只能提高20%（1/［（1－0.2）＋0.2/6]≈120%），如果提高处理器的性能，系统整体的性能能够提高25%（1/［（1－0.6）＋0.6/1.5]=125%）。有兴趣的同学可以自己验证一下。



2、接下来，如果一年后还要再推出一个新的系统，假定处理器和内存的性能提升的可能性和成本跟上一次相当，这回该改进计算机处理器，还是内存呢？

有人觉得还是该改进处理器，很遗憾，这一次该改进内存了。因为上一次处理器改进后，处理器运算占用的时间比例，也就是公式中的p，就从60%下降到50%了，再改进处理器，油水就没有那么大了。事实上，如果继续改进处理器，可以得到20％左右的性能提升，而改进内存这回能获得25%的性能提升。



3、阿姆达尔法则不仅是产品设计中选择技术的准则，更是整个计算机行业里决定研发投入依据的原则，也就是说，`当前如果计算机系统中的哪个部分成为了拖后腿的瓶颈，就必须集中精力和经费解决相应的问题，这也就解释了为什么IT的关键技术似乎都在合适的时间获得突破的原因。`





# 对于个人而言



对于个人而言，阿姆达尔法则也是我决定该做什么事情，不该做什么事情的原则。那些只能产生1%效果的事情，你就是把结果提高一百倍，影响力也有限；相反，那些占到了一半以上效果的事情，哪怕改进5%，至少我们能看到2.5%的整体提高。计算公式：

> 1/［（1－P）＋P/S]，如果p＝50%=0.5，S＝1.05, 代入后等于1.024，也就是可以提高2.4%，如果是一半以上的效果，就能有至少2.5%的提高，如果S＝101，P＝1%＝0.01，代入后等于1.009，得到的提升不到1%。

# See Also 

>* newpost 
>
```
/Users/devzkn/bin//newpost Why_the_IT_industry_is_progressing_so_fast IT行业为什么进步这么快?阿姆达尔法则（Amdahl Law） -t GoogleMethodology
> #原来""的参数，需要自己加上""
```

