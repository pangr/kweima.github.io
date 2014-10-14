---
layout: post
title:  正确初始化NSURL的方法
date:   2014-03-20 15:56:50
categories: [iOS Dev]
---
一般情况下，使用包含访问地址的NSString初始化一个NSURL的方法如下：

{% highlight objc %}
NSString *path = @"http://www.example.com/data.json";
NSURL *url = [NSURL URLWithString:path];
{% endhighlight %}

但是对于含有中文的地址，比如http://www.example.com/img/测试图片.png，用这样一个NSString去初始化NSURL就会失败，从而获取不到数据。正确初始化NSURL应该是：

{% highlight objc %}
NSString *path = @"http://www.example.com/data.json";
NSString *legalPath = [path stringByAddingPercentEscapesUsingEncoding:NSUTF8StringEncoding];
NSURL *url = [NSURL URLWithString:legalPath];
{% endhighlight %}
