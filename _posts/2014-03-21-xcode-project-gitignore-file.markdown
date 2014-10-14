---
layout: post
title:  "为Xcode工程添加.gitignore文件"
date:   2014-03-21 15:56:50
categories: [Xcode]
---
创建Xcode Project时，默认会为Source Control勾选上Create git repository，这样省去了自己创建Git的环节。但默认的Git会跟踪所有文件，包括一些隐藏的工程文件，而这些文件没有必要去跟踪，因为他们永远一个状态，几乎不会有变化。所以在创建工程时，不要勾选Create git repository，创建完工程后，在工程根目录创建.gitignore文件，将需要忽略的规则添加进去，然后再手动创建Git。

Xcode工程的参考.gitignore文件内容如下：

{% highlight vim %}
# Xcode
.DS_Store
*/build/*
*.pbxuser
!default.pbxuser
*.mode1v3
!default.mode1v3
*.mode2v3
!default.mode2v3
*.perspectivev3
!default.perspectivev3
xcuserdata
profile
*.moved-aside
DerivedData
.idea/
*.hmap
*.xccheckout
 
# CocoaPods
Pods
 
# Xcode Test Folder
ProjectTests/
{% endhighlight %}

其中最后一行为工程文件夹中的<YourProjectName>Test文件夹，需要改称你自己的文件夹名称。

然后使用git init来初始化一个Git，再使用git add .把文件添加到跟踪列表。
