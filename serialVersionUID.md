---
dfdfadf:
	ddfd:
	dfdf:
	ddfdf:
		
---

[TOC]

aaaaaa.bbbb=test

### serialVersionUID

序列化是将对象的状态信息转换为可存储或传输的形式的过程。
我们都知道， Java对象是保存在JVM的堆内存中的， 也就是说， 如果JVM堆不存在了， 那么对象也就跟着消失了。
⽽序列化提供了⼀种⽅案， 可以让你在即使JVM停机的情况下也能把对象保存下来的⽅案。 就像我们平时⽤的U盘⼀样。 把Java对象序列化成可存储或传输的形式（ 如⼆进制流） ， ⽐如保存在⽂件中。 这样， 当再次需要这个对象的时候， 从⽂件中读取出⼆进制流， 再从⼆进制流中反序列化出对象。
但是， 虚拟机是否允许反序列化， 不仅取决于类路径和功能代码是否⼀致， ⼀个⾮常重要的⼀点是两个类的序列化 ID 是否⼀致， 即serialVersionUID要求⼀致。
在进⾏反序列化时， JVM会把传来的字节流中的serialVersionUID与本地相应实体类的serialVersionUID进⾏⽐较， 如果相同就认为是⼀致的， 可以进⾏反序列化， 否则就会出现序列化版本不⼀致的异常， 即是InvalidCastException。
这样做是为了保证安全， 因为⽂件存储中的内容可能被篡改。
当实现java.io.Serializable接口的类没有显式地定义⼀个serialVersionUID变量时候， Java序列化机制会根据编译的Class⾃动⽣成⼀个serialVersionUID作序列化版本⽐较⽤， 这种情况下， 如果Class⽂件没有发⽣变化， 就算再编译多 次， serialVersionUID也不会变化的。
但是， 如果发⽣了变化，那么这个⽂件对应的serialVersionUID也就会发⽣变化。
基于以上原理， 如果我们⼀个类实现了Serializable接口， 但是没有定义serialVersionUID， 然后序列化。 在序列化之后， 由于某些原因， 我们对该类做了变更， 重新启动应⽤后， 我们相对之前序列化过的对象进⾏反序列化的话就会报错

------

