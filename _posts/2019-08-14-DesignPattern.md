---
layout: post
title:  Design Pattern 设计模式
date:   2019-08-14 01:08:00 +0800
categories: DesignPattern
tag: 笔记
---	

* content
{:toc}

Design Pattern设计模式 
------------------------------------
  "每一个模式描述了一个我们周围不断重复发生的问题,以及该问题的解决方案的核心.这样,你就能一次一次地使用该方案而不必做重复劳动"

4个基本要素
------------------------------------
1. pattern name 描述模式的问题，解决方案和效果
2. problems 应该在何时使用该模式
3. soulation 描述了设计的组成部分，以及他们之间的相互关系及各自的职责和协作方式
4. consequences 描述了模式应用的效果及使用模式应权衡的问题，


设计模式分类
------------------------------------
	创建型 Creatonal
		    Factory Method 
			Abstract Factory
			Builder
			Prototype
			Singleton
	结构型 Structural
		    Adapter
			Adapter
			Bridge
			Composite
			Decorator
			Facade
			Flyweight
			Proxy
	行为型 Behavioral
		    Interpreter
		    Template Method
			Chain of resposibility
			Command
			Iterator
			Mediator
			Memento
			Observer
			State
			Strategy
			Visitor



设计模式简介
---------------------------------
##### Abstract Factory
  提供一个创建一系列相关或依赖对象的接口，而无须指定他们具体的类

##### Adapter 适配器模式
  将一个类的接口转换成客户希望的另一个接口，从而使得原本由于接口不兼容而不能一起工作的那些类可以一起工作
  SpriveMVC 中 HandlerAdapter 
  DispatcherServlet 

##### Bridge 桥接模式
将抽象部分与它的实现部分分离，使他们都可以独立地变化

##### Builder 建造者模式
将一个负责对象的构建与他的表示分离，使得同样的构建过程可以创建不同的表示

##### Chain of Responsibility 责任链模式
为解除请求的发送者和接受者的接偶，从而使得多个对象都有机会处理这个请求，将这些对象连成一条链，并沿着这条链传递该请求，直到一个对象处理它。

##### Command 命令模式
将一个请求封装为一个对象，从而使你可用不同的请求对客户进行参数化，对请求排队或记录请求日志，以及支持可取消得操做

##### Composite 组合模式
将对象组合成树形结构以表示"整体-部分"的层次结构， 从而客户对单个对象和复用对象的使用具有一致性

##### Decorator 装饰者模式
动态地给一个对象添加一些额外的职责，就扩展而言 Decorator 比生成子类更灵活

##### Facade 外观模式
为子系统中的一组借口提供一个一致的界面， Facade模式定义了一个高层接口，这个接口使得这一子系统更加容易使用

##### Factory Method 工厂模式
定义一个用于创建对象的接口，让子类决定将那一个类实例化，FactoryMethod 使得一个类的实例化延迟到子类

##### Flyweigth 享元模式
运用共享技术有效地支持大量细粒度的对象

##### Interpreter  解释器模式
给定一个语言，定义它的文法表示，并定义一个解释器，该解释器使用该表示来解释语言中的句子

##### Iterator 迭代器模式
提供一种方法访问一个聚合对象中各个元素，而又不需要暴露该对象的内部表示

##### Mediator 中介者模式
用一个中介对象来封装一系列的对象交互。中介者使各对象不需要显示的相互应用，从而使其耦合松散，而且可以独立地改变他们之间的交互

##### Memento 备忘录模式
在不破坏封装性的前提下，捕获一个对象的内部状态，并在该对象之外保存这个状态，这样就可将该对象恢复到保存的状态。

##### Observer 观察者模式
定义对象间的一种一对多的依赖关系，以便当一个对象的状态发生改变时，所有依赖于它的对象都得到通知并自动刷新

##### Prototype 原型模式
用原型实例制定创建对象的种类，并且通过拷贝这个原型来创建显新的对象

##### Proxy 代理模式
为其他对象提供一个代理以控制这个对象的访问

##### Singleton 单例模式
保证一个类仅有一个实例，并提供一个访问他的全局访问点

##### State 状态模式
允许一个对象在其内部状态改变时改变它的行为，对象看起来似乎修改了他所属的类

##### Strategy 
定义一系列的算法，并把他们一个个的封装起来，并且使他们可相互替换，本模式使得算法的变化可独立使用于其他的客户

##### Template Method 模板模式
  定义一个操作中的算法的骨架，而将这一些步骤延迟到子类中， Template Method 使得子类可以不改变一个算法的结构即可重新定义该算法的某些特定步骤
  JDK 中 锁 ReentrantLock 中 AbstractQuenedSynchronized 就使用了模板模式
##### Visitor 访问者模式
表示一个作用于某个对象结构中的各元素的操作，它使得你可以在不改变各元素的类的前提下定义作用于这些元素的新操所，



 
