---
layout: post
title: How_to_use_good_computer_thinking
date: 2018-10-30
tag: GoogleMethodology
site: https://zhangkn.github.io
catalog: true
author: kunnan
subtitle: 如何用好计算机思维?
---



# 前言



* `所以在计算机世界里面，常常不是对和错、好和坏的事情，而是给定了固定成本以后你怎么做，常常边界确定了，你所能做的事情也就确定了。` `好的从业者要有成本和性能的意识，而不是简单的好坏、对错。`



## 一、怎样做一个合格的工程师？





1. 第五级是一个合格的工程师。你做到一些对于工程师最基本的要求的时候，你就合格了，也就是达到第五级了，如果连第五级都做不到，那就是不入流的工程师。
2. 第四级是你可以带领几个徒弟共同完成一件事。这已经是一个“网络”的行为了，就需要有一点领导力了。
3. 第三级，如果是在谷歌里面，就相当于能负责一个产品线，比如说你负责地图，地图里面有一些跟地面数据和卫星的图象能够重合，卫星的产品是你负责的，或者说导航是你负责的。
4. 第二级，你能够做出世界上其他人做不出来的东西。
5. 第一级：开创一个产业



第五级，合格不合格的问题，一个工程师你做完了，要满足三个属性，

*  第一，经常能工作，不要老坏。
*  第二，可继承。万一你不在了，或者离开公司，哪怕死掉了，这个事还能有人接着做，不能说中断了，一个文明的进程是不断继承的过程，工作不断从零开始，没有积累，效率太低，这是第二条，第一个是你做出来的本身可用。
*  第三，打好包，封装好，人家可以在你这上面做进一步的工作。不仅工程师如此，任何一个职业人士，这是三个最基本的素质。

#### **第一，如何让你做出来的东西能持续工作？**

比如说做一件事的时候，他们要保证把这一件事做好，而不是仅仅把其中的一小件事情做好。

* ·比如说一个游戏，从设计到功能、测试、封装、提交，以及到后来的很多维护，都要一个人自己做。用硅谷很多公司的话说，自己做的事情要自己收尾。
  * 但是，从现在分工的角度讲，为什么测试不能交给别人做？
    * 因为没有人写代码是能够完全正确的，到目前为止世界上被证明水平最高的人可能是高德纳，他一辈子写代码，被人发现只有个位数的错误，但是其他人写的所有代码都被人不断地发现错误，如果你不测试，可能用不了几天就死掉了。`测试不测试，是看这个人是否是一个职业化的人的很重要的一个原则。`

* 小学生都知道，交卷以前要检查，自己不测试，可能连小学生都不如。
  * 在美国，我个人和我们公司用的会计师都非常好。他们每年给我们提供税务工作，我发现他们每个人都有一级一级非常严格的自查流程。即使这个会计师事务所的收费是其他事务所的三倍，那也是因为它做了其他事务所做不到的事情。



**第二，你做的事情是要能够继承的。**你总要留下一些遗产，如果你离开一个公司以后，回头有五个人告诉你说，我们现在用的还是你的代码，你就会很高兴。你前脚刚走，后脚就有人说，终于把这个质量很烂的东西删掉了。你就没有什么成就感。这就是第二个属性，有可继承性。



**第三，在你做的东西的基础上还可以发展，**比如说很多的程序是开源的，上面可以做各种各样的变种、子操作系统，或者是新的UI界面操作系统。能够做到这一点，你的成果才会被最多的人使用，你自己才有成就，获得最大的收益。



#### 相当于师父一样，带一个小团队，你怎么把这个团队带好？







**首先，自己要建立一个规范，**当你自己一个人做事情，你能够理解你全部的意思。你带领十个人做事情的时候，就需要一个规范。如果没有一个规范，这十个人就没有共同讨论的基础。这个时候，给你的人数越多，你管理起来越辛苦。

* 汉朝有一句话：韩信将兵，多多益善。但是对于很多领导来讲，带的人越多，他越乱。你要制定一个规则，让大家都来遵守，这才是合格的职业人应该做的事情。
* 医生有医生的规范，律师有律师的规范。做到这一点，在中国这样一个环境中有非常大的发展机会，因为如果你做到这一点，别人做不到这一点，你就有非常大的机会。
* 很多人说赢在起跑线上，你不用在起跑线上那么辛苦。因为在规范性这一条上，80%的人做不到，只要你做到了，你就赢了80%的人。关于领导力（递归、分治）的问题，稍后会讲。





## [二、我们怎么把计算机思维应用在我们的工作中？](https://kunnan.github.io/2018/04/22/TheWayOfThinking/)



什么叫计算机的思维方式？其实人类有些知识是共通的，人类在设计计算机程序的时候，汇聚了一些智慧，你在生活中也可以用。



#### **1.递归**

计算机里面有一个名词叫递归，还有一个名词叫分治。

* 递归，就是以前小孩子都说的一句话：“从前有个山，山里有个庙，庙里有个老和尚在讲故事……”不断讲下去。在计算机里常常遇到很大的问题，这个问题不好解决，怎么办呢？就变成一个跟它原来很相似的，比原来规模小一点的问题来解决。第二个小一点问题的解决方式寄希望于什么办法呢？也是通过跟它有点相似的，但是规模再小一级的，一级一级到最后一个个体的时候，就好解决了。

这个在管理中很有用。一个人怎么管好他的下属呢？很简单，有两点。

**第一，树榜样，你怎么做，下属也怎么做。这一点很重要。**

**第二，你只管好你的下属，**至于下属的很多事，你不要太操心，由他们自己来管。一个公司的总经理管好下面每一个部门的总监就好了。

你树立了一个榜样，这个榜样是一个规矩，下面的人也跟你一样执行这个规矩，每个星期每个人都要跟你做一次交流，谈半个小时，介绍一下工作。每星期你要组织大家开一次会，大家讨论一些问题。

至于你下面的总监，每个人下面还有20个产品经理，或者其他的工程经理。他们就学你，你跟每个总监交流，他们也跟下面的每个经理交流，也组织一些经理开会；下面的经理就跟小组长们一对一地交流，组织大家开会；小组长们再跟下面的每个员工交流，一级一级地管起来，这样一个大的机构就可以管起来，你就可以管一千个人。

如果你没有这样一个清晰的机构，一千个人管理起来就很费劲，一会儿这儿出问题，你像一个救火队长一样冲过去了。

**很多人问我，你怎么培养领导力？** 

* 这一点就叫做递归，在领导力上叫做授权，最糟糕的是事无巨细，就像诸葛亮一样，事必躬亲，自己累死也未必能把事情搞好，一个领导再厉害，也不能把所有事情都做得在行，最主要的是发挥下面人的才智。
  * 很多人在一个单位干了十几年也不能得到提升。他自己是一个技术尖子，干得很好，但是不知道把这个事情教给下面的人做好。很多人说，与其教他们做，还不如自己来。但是如果所有事自己来，一个人再能干，也只是一个人的力量，如果教会了十个人，就是十个人的力量，十个人如果再有领导力，每个人教会了十个人，就是一百个人的力量。

这就是递归的力量，一旦一个组织架构建立起来以后，下面每一级的人就学着上面老板做事。如果老板眼睛只盯着KPI，那么下面所有经理、总监都会这样做。如果老板从来不提倡合作，下面的所有员工也不会提倡合作。

* 所以一个创始人的基因常常决定了一个企业的基因。
  * 投资的时候经常要看一个创始人合适不合适。创始人如果不合适，造成一个很坏的基因，这个公司哪怕做的事情再好，最后也难以成功。事情合适，但是人不合适，这件事情几乎一定是不成功的。

`这是讲的递归，是很简单、很偷懒，也很有效的管理方式。很多人问我，你哪有时间干那么多事？我说很简单，就是授权，把自己的权限授权下去，给下面做一个榜样，下面被授权的人就按照你的模式来做事情了。`

#### **2.分治**



一个大问题的复杂度比十个小问题要大得多。但是如果你有本事把一个复杂的大问题，拆解成十个相对并不关联的小问题的话，就要容易得多。因为能够处理解决大问题的人是很少的，能够解决相对小的问题的人是很多的。

* 比如说写一百万行代码的大系统，能够负责这样一个项目的总架构师其实不多。但是如果你有本事把它拆成十个十万行的项目，你在社会上还是能请到十个这样的人。

* 在一个企业里面，很多人说，我是不是把很多牛人凑在一起，这个事就能做成？不是的。很多时候是你要找到一个合适的拆解办法，把你的大的工作拆解成十个小的工作。这十个小的工作你要找到能够胜任的人来做。这就比较合适了。因为杀鸡用牛刀，把很重要的人放在不太重要的位置上，这个人的产出不一定很高。

`这是今天企业管理很重要的原则，相应岗位的人要相匹配`。对于一个大问题，要有拆解的能力。一个人一下子从第五级的工程师上升到第三级，我刚才讲的方法就很重要，用分治法，把大问题拆成小问题。

* 你要到英国去玩，这么大的问题，你肯定要拆解，办签证、买机票、订酒店、准备食宿、看什么景点可以玩、看天气、准备照相器材。有的人是胡子连着眉毛一把抓，最终总是丢三落四。今天面对的问题比以前要大得多。

`这两个重点我再强调一下，一个是分治，一个是递归，它们两个可以结合起来使用，把大问题拆成小问题，找下面合适的人做，立下自己的规矩，把自己的工作方式方法传达下去，整个企业就会有一致的文化，也就能获得一个很强的合力，大家能够往前发展得更好。`



#### **3.对立统一**



在计算机里面，我讲了计算机的一些相互对立统一的关系，比如说我讲大和小的对立统一，快和慢的对立统一，多维度和单一维度的对立统一。计算机是一个网络效应，人是个体效应。

今天我们讲人工智能，而计算机和人的一个很大的区别在于，人的思维是相对独立的，互相不影响的，有合作意识的。计算机获得智能的方式是通过搜集到大量的数据、得到一个综合的结果，具有很强的网络效应（非连续性的）。

这是一个很大的差别。这也是为什么在很多地方我们发现基于大数据的人工智能做的事情比人能做得好。同样，人如果脱离掉自己完全独立的、只考虑自己的做事方式，而能够兼顾很大的网络，也会得到很好的效果。

#### **4.全局和局部**



我们经常会听说，有一支军队，赢了每一场战斗，输掉了整个战役。或者有的人，输了每一场战斗，但是赢了整个战役。人认识的世界是一个相对小的世界。

比如说个位数，今天你认识起来没有问题，十位数也数得很清楚，但到了几千几万几亿的时候，是完全无感的。计算机要处理的世界比这个要大得多得多。

* 举一个例子，你问一下世界上最大的数字是多少？有人会说无穷大，无穷大不是一个有意义的数字。10的一百次方，这个数字比全宇宙所有的基本粒子的数量不知道大多少亿倍。整个宇宙的粒子基本上也就是10的80次方。

* 今天计算机加密就需要一个非常大的素数，或者叫质数。计算机从一开始就是处理很大的数，它和人对大小的理解不一样。

**很多时候我们说，抓大放小容易，但是人做事都是从小到大一点一点积攒，聚小变大。计算机做事和人做事的差别是什么？领导考虑问题和个人考虑问题有什么差别？** 

`前者基本上是自顶向下，先考虑一个非常大的整体，底下的东西都是不精确的，先把几个大的整体模块定义清楚，然后再往下一级一级地细化。`

这是计算机的做事方式。我们人做事常常是反过来。业余的人写作文，都是从细节开始一点一点写下去。比较专业的人写作，会先构思整个故事的情节。这就是业余人的做法和专业人的做法的差别。

** 因为计算机精度有限，只有32位，甚至有些时候只有8位，怎么能表达一个数字？**   我们通常想，一个数字的表达越准确越好，你学数学的时候并不觉得位数是一个问题，如果你自己觉得算不过来了，老师会说，算到小数点后四位就可以了。

计算机中只有8位。如果表达一个数字，只有从0表达到255，如果要表达几万怎么办？或者一个8位的二进制能不能表达几十万？原则上来讲是可以的。在这里就要有一个牺牲，但在数量级上要保证基本是对的。

接下来，如果只有八位，我只能保证数量级是对的。如果还有内存，可以再给你8位、16位，我可以保证数量级是对的，精度也是对的，这个计算机就合适了。`计算机的世界是一个完全离散的世界，不是连续的，甚至不是精确的，它是一个大致的、在我们能够接受的误差范围内的工程的解决方案。`

* 我们在生活中常常也会遇到这样的问题，比如你跟朋友出去，他帮助你买火车票，花了1345块，你常常给他1350块，或者给他1400块。我们注意大，不要费工夫抠细节，如果细节抠得太细，有时候反而失去了我们本来能够掌握的一些大局，所以这是计算机的先大后小的关系。再讲它的小，有些时候精度特别高，用计算机算出来的世界上最大的素数，有几千万位，光数量级对了没有意义，那怎么办？
  * 首先在大致的范围内要确定，原来最大的素数已经到多少位了，现在要超过它，大概要到多少位。第二，它要把很多小的资源合并起来，处理一件大的事情。这就是它的大和小的辩证关系。







`所以，很多时候建议大家换一个思维方式，从上往下，从大往小来思考。先不要关注细节，大的局势定了以后，再关注细节。`





## 三、如果癌症攻克了，我们人类的寿命会提高多少年？



因为从现在的科学研究结果来看，人最多不会超过120岁。现在人的平均寿命已经接近80岁了。有些人认为能够多活10岁或20岁，也是不可能的。答案是3.5岁。



这是谷歌下面大数据医疗公司Calico的CEO亚瑟·莱文森给出的答案，他是现在苹果董事会主席，所以给出的答案是很权威的。

我们忽略了一点，全世界得癌症的人只有百分之十几，李光耀得了癌症，但他活了几十年，还有一些人基本上是治好的。



#### 什么问题不要光问对和错，计算机世界里很多时候没有对和错，只有好和不好，以及在同样的成本下，什么是最好。

* 比如说今天给你一万元，你去买一个苹果电脑，怎么选配置比较好？你说内存大一点，或者是CPU快一点，哪一个更好？学过一点计算机的人说，内存大一点好，因为计算机的CPU提升10%或者20%，这个价钱换内存能够快一倍，可以同时很好地运行很多大程序。
  * 对很多人来讲，肯定是增加内存，当然这事也不一定。因为对于某些特殊的人，他对内存不一定很需要，他就希望速度快一点就好。这是在做计算机方面很重要的思维，在生活中也是这样。

* 年轻人讲，希望选一个太太，并提出10个要求，我说你肯定找不着，这样的人首先不一定存在，就算存在也未必看得上你，因为她也可以提十个要求，你一定不能满足她这十个要求的，这件事是不太可能发生的。

`很多时候我们在生活中会幻想一个理想状态，但是在工程中我们要想一个实际的状态。比如说前一阵子贸易战开始，很多人爱国情绪高涨。很多人说，中国为什么不造CPU？我们造一个CPU，性能超不过美国吗？`



咱们也造得出来。用刚才那个逻辑来分析一下，就是成本问题。首先，如果你将来的CPU造价是现在通用的10倍。大家会不会买？你可以说，没有关系，大家都爱国，宁可每个手机的价钱贵一千块钱，我也买。

但是再接下来，有了这个CPU以后，用什么操作系统？是继续用安卓的，还是你说，操作系统我也不用安卓的了，我要自己开发一个。

现在华为是用自己的CPU，用的安卓操作系统。它的CPU花了很长时间才跟安卓绑定、一致、优化。现在基本上CPU和操作系统很难分开。英特尔和微软经过了很长时间的磨合，才磨合出比较好的整体效果。单纯开发操作系统，价格贵不说，整体效果还不好。

如果你要做操作系统，先不说能不能做出来比微软更好的操作系统，就算做出来以后，哪来的软件？你可能说我再开发软件，但是问题是，中国现在没有形成一个很大的付费的软件市场。你可能未必有钱养所有的软件公司。如果没有那么多软件，你的操作系统也生存不下来。

`这已经不是对和错的问题，或者好和不好的问题，或者说绝对性能高和低的问题。而是在我们现有的成本下，能否做到性能最好、大家都接受的东西，在计算机里面考虑的是这一点`。这一点和航天不一样，在航天领域我砸钱搞一个性能最高的火箭，那么我的性能就是比其他的好。

我们看今天的Office比二十年前好不到哪去，我们不能做出一个比微软更好的软件吗？不是做不出来更好的，而是你做出来了，很可能因为性价比的问题，以及和其他周边配套技术的问题，以至于没有人用，这是一件很不划算的事情。

而微软的操作系统，只是说它已经足够好了。在目前的情况下，对PC机来讲，同样成本的情况下，是大家最能接受的。`所以在计算机世界里面，常常不是对和错、好和坏的事情，而是给定了固定成本以后你怎么做，常常边界确定了，你所能做的事情也就确定了。`







通过讲这些，希望能够给大家回答两个问题，第一，为什么不能做一个取代英特尔或者ARM的芯片？有时候我们觉得理工男很爱钻牛角尖，因为他们只想到一面。而这恰恰是我们这一节课要改变的，`好的从业者要有成本和性能的意识，而不是简单的好坏、对错。`



# See Also 

>* [<吴军的谷歌方法论>之'计算机思维‘](https://kunnan.github.io/2018/04/22/TheWayOfThinking/)
>* newpost 
>
```
/Users/devzkn/bin//newpost How_to_use_good_computer_thinking 如何用好计算机思维? -t GoogleMethodology
> #原来""的参数，需要自己加上""
```
