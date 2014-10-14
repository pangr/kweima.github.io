---
layout: post
title:  声明属性为weak还是strong
date:   2014-03-20 16:56:50
categories: iOS Dev
---
前几日测试App，发现内存分配一直在增加，但是不会被释放，来回切换几个视图内存就会暴增。我特意手贱一直狂点，然后App崩溃。 代码使用了ARC。之后一直在找问题所在，程序中很多地方使用多线程，修改几遍发现也不是。终于发现是delegate的strong引用出了问题。

我有一个ViewController，里面有两个property，一个是mainModel用来提供数据，一个是mainView来布局，都是strong引用。然而，在mainModel里，我又定义了一个delegate，当mainModel发生错误的时候，会调用delegate遵守的protocol方法，来解决错误。在ViewController里，初始化mainModel后，将其delegate设置成了self。

问题来了，ViewController对mainModel有strong引用，mainModel中通过delegate对ViewController也有strong引用。因此产生了循环strong引用。继而内存不会被释放。

开始学Objective-C时，官方文档中就特意介绍过这种情况，后来我自己也在笔记本上记录过。这次还是疏忽了。一般来说，有两种情况需要使用到若引用。一种就是前面所说的delegate。另一种是子视图（subview）当把子视图添加到父视图之后，父视图对子视图自动就有了strong引用，如果学需要在子视图中引用父视图时，就需要weak引用了。
