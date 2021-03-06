---
title: javascript设计模式-单例模式
date: 2017-6-23 23:13:58
tags: 设计模式
---

用单例模式创建一个独一无二的对象，常常用来管理共享的资源，例如数据库链接或者线程池，另外也可以确保某个资源在全局只有一份。简单的单例模式，配上惰性的特性，在开发中具有非一般的实用性。

#### 定义

保证一个类仅有一个实例，并提供一个访问它的全局访问点。

#### 实现

利用一个变量来标志当前是否已经为某个类创建过对象，并且不直接用new来得到一个实例，而是通过类似getInstance的方法来获取对象实例。

```javascript
var Singleton = function() {
  this.instance = null;
}
Singleton.protype.getInstance = function(){
  if(!this.instance) {
    this.instance = new Singleton();
  }
  return this.instance;
};
var a = Singleton.getInstance();
var b = Singleton.getInstance();
console.log(a===b); // true
```

思考：那么如何避免别人来实例化多个呢？上面的代码的确我可以new多个。

java中的做法是不公开构造函数，即给构造器添加private关键字。javascript则可以用闭包来实现私有的效果。

#### 针对JavaScrpt的单例模式

在js中我们可以通过使用全局变量来实现单例模式的效果。我们在全局可以创建一个对象，让代码中的任何为止都可以访问，从而通过判断该对象是否初始化来实现单例模式。但是实际中，全局变量存在很多问题，比如命名空间污染。那如何降低js全局变量带来的命名污染？有以下几个方法：

1. 使用对象字面量

   ```javascript
   var namespace = {
     a: function(){...},
     b: function(){...}
   }
   ```

2. 使用闭包封装私有变量

   ```javascript
   var a = (function(){
     var __instance = new Singleton();
     return {
       getInstance: function(){
         return __instance;
       }
     }
   }) ();
   ```

#### 惰性单例

然而，实际开发中我们还可以使用单例模式，在只在需要它的时候才去创建实例，这类单例叫做惰性单例。

比如网页的登录框，它不仅是唯一的（不可能同时出现两个登录框），所以这里就很适合用单例模式。而且如果用户不点击登录按钮进行登录，它就不会现身，so我们为了加快页面加载的速度，应该等到需要它时才去实例化。

将创建对象和管理单例的职责分别放置于两个方法中，组合使用的话能让单例模式的使用更加符合单一职责原则。

#### 感叹

在设计模式中，经常能听到我们需要把变和不变的部分隔离出来，把业务逻辑和业务无关的逻辑隔离出来。学习设计模式的这几天，看书看别人举例子都觉得好奇妙，好简单的样子，然而等我跃跃欲试想拿着自己学到的这几个模式去重构以前写的代码时，深刻发现实际开发的使用其实并没有现象中那么简单，你需要辨别如何把代码隔离出来，做到可复用的同时又做到易读性。尽管对我来说，写出优美代码这条路长路漫漫，但是通过学习设计模式才体会到写代码真的是一件有意思的事情啊！