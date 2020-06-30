---
layout: post
title:  "UE4对象模型-UObjectBase"
date:   2020-06-30 19:42:37 +0800
categories: jekyll update
---
UObject对象模型目前分层了三层继承关系：UObject -> UObjectBaseUtility -> UObjectBase。

UObjectBase有如下成员字段：
{% highlight C++ %}
class UObjectBase
{
  EObjectFlags ObjectFlags // 对象的Flag，源码中注释非常清晰，这里不赘述。
  int32 InternalIndex // 所有UObject对象都会放在FUObjectArray中，这个是下标。
  UClass* ClassPrivate // 这个UObject的对应的UClass
  FName* NamePrivate // 这个对象的名称
  UObject* OuterPrivate // 这个对象的归属的UPackage
  }
{% endhighlight %}

自定义对象模型，我认为有如下几方面需要考虑：
* 内存管理，如何GC，如何计算引用。
* 与脚本层的交互，也就是如何实现C++与蓝图，或者任何一门脚本语言的交互。
* 序列化