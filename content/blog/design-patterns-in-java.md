---
title: "Design Patterns in Java"
date: 2019-10-22T14:04:38+05:30
draft: false
tags: ["design patterns"]
---

<img src="https://i.ibb.co/9Gb6KV7/Design-Patterns-in-Java.png" alt="Design-Patterns-in-Java" border="0">

Design patterns in java are best practices which are used to resolve some known issues.  Design patterns can be divided into 3 different types. Here we have listed down some of the widely used design patterns in Java.

<ol>
<li><a href="#singleton">Singleton Design Pattern</a></li>
<p>
You must have heard about the Singleton Design Pattern. One of the most common question in Interviews. So here in this article, we will discuss Singleton pattern and try to resolve all queries you might have for Singleton pattern…….
</p>

<li><a href="#factory">Factory Design Pattern</a></li>
<p>In this article, I will write about the Factory Design Pattern why it is good and how to use it when writing a Java application.</p>
<li><a href="#decorator">Decorator Design Pattern</a></li>
<p>In this article, I write about the Decorator Design Pattern. This is a very nice pattern if you want to extend class behavior at runtime.</p>
<li><a href="#composite">Composite Design Pattern</a></li>
<p>
In this article, I’ll introduce the Composite Design Pattern. This pattern is used to represent part-whole hierarchies.
</p>
<li><a href="#adapter">Adapter Design Pattern</a></li>
<p>
In this article I’ll introduce the Adapter Design Pattern and how you can use it in Java. This pattern is mostly used to enable loosely-coupling of plugins into applications (for example the way Eclipse does this).
</p>
<li><a href="#prototype">Prototype Design Pattern</a></li>
<p>
This pattern is a creational pattern (just as the already introduced Factory Pattern) and it comes to play where performance matters. This pattern is used when creating a new object is costly: you use a prototype and extend it with the particular implementations of the needed object.
</p>

<li><a href="#facade">Facade Design Pattern</a></li>
<p>
A facade is for hiding features from external clients and to give them a unified access point to public functionality.
</p>

<li><a href="#proxy">Proxy Design Pattern</a></li>
<p>
In this article, I’ll write about the Proxy Design Pattern. This pattern is used to control access to resources and objects. The real value of this pattern is to reduce memory costs for objects until you really need them.
</p>

<li><a href="#iterator">Iterator Design Pattern</a></li>
<p>
In this article I’ll write about the Iterator Design Pattern. This pattern is used to iterate over an aggregate object without exposing the underlying implementation of this object.
</p>
</ol>

<p><a name="singleton"></a></p>

### What is Singleton Design Pattern?

<p>If you are in Java then you must have used the new keyword. This new keyword creates an Object of class whenever required. But there are some scenarios where you don’t want to create individual Object for a different purpose. Singleton Pattern ensures that one and only one Object is instantiated for a given class. Whenever an object of a given class is required, only single(No more than one object) Object get returned.</p>

#### Implementation of Singleton Design Pattern

Now you know what is the Singleton Design Pattern. Next step would be to implement it. There are different ways you can implement Singleton. Before you start implementation, you need to understand what are the different ways to create an Object.

##### Different Ways to create an Object

<ul>
<li>`new` Keyword </li>
<li>Using `the New Instance` (Reflection)</li>
<li>Cloning of an Object</li>
<li>Using Class Loader</li>
<li>Using Object De-Serialization</li>
</ul>

<p><a name="factory"></a></p>
<p></p>
<p><a name="decorator"></a></p>
<p></p>
<p><a name="composite"></a></p>
<p></p>
<p><a name="adapter"></a></p>
<p></p>
<p><a name="prototype"></a></p>
<p></p>
<p><a name="facade"></a></p>
<p></p>
<p><a name="proxy"></a></p>
<p></p>
<p><a name="iterator"></a></p>
<p></p>