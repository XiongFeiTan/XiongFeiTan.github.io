---
layout: post
title: proxy 模式  
comments: true
categories: [java, design model]
tags: [java]
description: the basic of the proxy design model .
---

{{ page.title }}
================
<p class="meta">12 Jan 2016 - xiangtan</p>

<hr />
# 代理模式

---

* 代理模式：
代理模式通过代理目标对象，把代理对象插入到客户和目标对象之间。代理对象可以在调用具体的目标对象前后，附加很多操作，从而实现新的功能或是扩展目标对象的功能。

静态代理：代理对象，要实现与目标对象一样的接口。
* Proxy：
实现与具体的目标对象一样的接口，就可以使用代理来代替具体的目标对象。
保存一个指向具体目标对象的引用，可以在需要的时候调用具体的目标对象，可容易控制对具体目标对象的访问，并可以负责创建和删除它。
subject:
定义代理和具体对象的接口，这样就可以在任何使用具体对象的地方使用代理对象。
RealSubject:
具体的目标对象，真正实现接口的功能.


动态代理（接口代理）：代理对象，不需要实现接口，代理对象的生成，利用JDK，API，动态的在内存中构建代理对象，需要指定创建代理对象实现的接口类型。
代理对象不需要实现接口，但目标对象要实现接口。
可以使用一个Handler代理多个接口的操作对象。操作java.lang.reflect.InvocationHandler接口。

---

* 从Class等API取得类信息的方式就称为反射。

Java真正需要某个类时才会加载对应的.class文档，而非在程序启动时就加载所有类。
java.lang.Class 的实例代表Java应用程序运行时加载的.class文档。Class用来包含类，接口，等信息，Class类没有公开public构造函数，实例是由虚拟机自动产生的，每个.class文档加载时，虚拟机会自动生成对应的Class对象。
通过同一类加载器载入的.class文档，只会有一个对应的Class实例。

Class.forName(String name);指定类名称来动态加载类。
Class.forName(String name,boolean initialize,ClassLoader loader);
默认加载.class文档时会执行类中定义的static区块，但这里可以将initialize设置为false，这样加载.class文档的时候并不会立即执行static区块，而会建立类实例时才执行static区块。

---
getClass()   
取得Class对象后，就可以获得里面的信息。

---
从Class建立对象
知道类名，可以new关键字建立实例，不知道类名称，则可用Class.forName()动态加载.class文档，取得对象后，利用newInstance()方法建立类实例。

---

BootStrap Loader --> Extended Loader --> System Loader 顺序寻找类。由Class的getClassLoader()加载对应的.class文档的classLoader实例。

---

