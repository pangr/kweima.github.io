---
layout: post
title:  Lazy Initialization in Objective-C
date:   2014-03-20 17:56:50
categories: iOS Dev
---
在创建自己的类时，有时候会重写init方法，而格式一般如下：

{% highlight objc %}
- (id)init
{
	if (self = [super init]) {
		 // Custom initialization
	}
	return self;
}
{% endhighlight %}

自定义类必然少不了新添加的属性，很多人喜欢在重写的init方法中去初始化这些属性：

{% highlight objc %}
@interface MyClass : NSObject
 
@property (strong, nonatomic) NSMutableArray *list;
 
@end
 
@implementation
 
- (id)init
{
	if (self = [super init]) {
		_list = [[NSMutableArray alloc] init];
	}
	return self;
}
 
@end
{% endhighlight %}

这样做中规中矩，但是有很大一个缺点，就是在初始化一个类时，类中所有属性都一并分配内存空间并初始化了。而有些属性当前不会不到，或者很久的将来也不会用到，早早的分配内存难免会浪费。更好的初始化方法时重写getter方法：

{% highlight objc %}
@implementation
 
- (NSMutableArray *)list
{
	if (!_list)
		_list = [[NSMutableArray alloc] init];
	return _list;
}
 
- (id)init
{
	if (self = [super init]) {
		// Custom initialization
	}
	return self;
}
 
@end
{% endhighlight %}

重写getter方法后，在调用属性的getter方法时，会检查当前属性是否是nil，如果是nil则初始化它，否则便返回该属性。这样在init方法中，就不会过早的分配内存，而是等到什么时候用，什么时候分配。大大优化了内存使用。
