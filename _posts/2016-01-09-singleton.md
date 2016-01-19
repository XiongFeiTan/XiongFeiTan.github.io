---
layout: post
title: singleton
categories: [java, design model]
comments: true
---

# singleton

---

* definition 

单例模式确保一个类只有一个实例，并提供一个全局访问点

* explanation

从定义可以看出，特点是这个类只有一个实例。why？有些时候，这个类只有一个实例会节约资源，或者只有一个实例才能保证整个程序运行正确，一致。例如：缓存，对话框，日志对象,线程池，等等 。


* example

```java
class Singleton {
	   private static Singleton singleton;

	   private Singleton() {
	}

	public static Singleton getInstance() {
		if (singleton == null) {
			singleton = new Singleton();
		}
	return singleton;
	}
}
```

这是单例的经典使用方式：

* 1. 一个 private static 对象

* 2. 构造器设置为 private
* 3. 一个 public static 方法提供全局访问点 

开始的时候，其实我比较困惑为什么不在 singleton 声明处直接实例化对象，后来明白了，这是一种延迟实例化的手段，保证只在需要时才实例化。如果直接在声明时实例化，那么只要类加载了，即使不需要对象，也会对它进行实例化。

另外，这个经典使用方式其实是有问题的，对比后面 Tomcat 中的应用场景，你可能会发现问题所在。

在 Tomcat 中，就有一个单例模式，它是 `org.apache.catalina.tribes.util.StringManager` 类。在 Tomcat 中，会有许多地方需要对错误消息进行处理。我们使用 `StringManager` 类来管理这些错误消息。

错误消息首先不能硬编码到代码中，否则需要提供国际化支持时，就会很痛苦。错误消息需要定义在配置文件中。Tomcat 为每个包 (package) 都提供了三种语言的错误消息配置文件。每个包内都有很多类，我们没必要为每个类都生成一个 `StringManager` 类，因为它们共享同一个配置文件。所以，一个包只需要一个 `StringManager` 对象就好了。我们怎么为一个包生成一个 `StringManager` 呢？ Tomcat 在 `StringManager` 内部保存着所有包的 `StringManager` 实例，你需要一个实例时，只需要提供包名，调用 `StringManager` 的相应方法，就会返回与此包名对应的 `StringManager` 实例。
