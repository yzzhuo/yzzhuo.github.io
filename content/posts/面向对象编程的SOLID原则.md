---
title: 面向对象编程的SOLID原则
date: 2017-7-8 23:13:58
tags: 设计模式
---

Javascript虽然与传统的面向对象编程语言Java有所不同，但是其设计模式都是围绕着SOLID原则，以便更容易创建可维护和可拓展的系统。

- 单一职责原则（SRP）：表明软件组件（函数、类、模块）必须庄主与单一的任务（只有单一的职责）
- 开/闭原则（OCP）：表明软件设计时必须时刻考虑到（代码）可能的发展（具有的拓展性），但是程序的发展必须最少地修改已有的代码（对已有的修改封闭）
- 里氏替换原则（LSP）：表明只要继承的是同一个接口，程序的任意一个类都可以被其它类替换。在替换完成后，不需要其它额外的工作程序就能像原来一样运行。
- 接口隔离原则（ISP）：表明我们应该将那些非常大的接口（大而全的接口）拆分成一些小的更具体的接口，这样客户端就只需关心它们需要用到的接口。
- 依赖反转原则（DIP）：表明一个方法应该遵从依赖于抽象（接口）而不是一个实例（类）的概念。