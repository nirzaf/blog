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

To make a singleton class you have to disable all these ways to create an object. One way to achieve this is to make the constructor of a given class private. But when you make the constructor private there is no way to create even a single object of the class.  So first make a constructor private and then prepare a way to create an object(Single) of that class.

##### Implementation One
Here we will create a private Constructor and also a static method to create an object of the same class.

{{< highlight java>}}
class JBT {

	/*
	 * This variable will be used to hold reference of JBT class.
	 */
	private static JBT instance = null;

	/*
	 * As private constructor is used so can not create object of this class
	 * directly. Except by using static method of same class.
	 */
	private JBT() {

	}

	/*
	 * This method will be used to get instance of JBT class. This method will
	 * check if there is aready an object of class create or not if not then it
	 * will create an Obect of JBT class and return the same else it will return
	 * the existing Object.
	 */
	static JBT createInstance() {
		if (instance == null){
                     instance = new JBT();
                     return instance;
              }
		else
			return instance;
	}

	int i;
}
{{< /highlight>}}

##### Problem
What will happen if 2 different thread enters the createInstance method at the same time when the instance is null. In that case, threads will create 2 different objects of JBT. Which is against the Singleton pattern. In the next approach, this problem can be solved.

##### Implementation Two
In this approach, we will make createInstance method synchronized so only one thread is allowed in that class and only one object will be created instead of Two.

{{< highlight java>}}
class JBT {

	/*
	 * This variable will be used to hold reference of JBT class.
	 */
	private static JBT instance = null;

	/*
	 * As private constructor is used so can not create object of this class
	 * directly. Except by using static method of same class.
	 */
	private JBT() {

	}

	/*
	 * This method will be used to get instance of JBT class. This method will
	 * check if there is aready an object of class create or not if not then it
	 * will create an Obect of JBT class and return the same else it will return
	 * the existing Object.
	 * 
	 * Now method is marked as synchronized hence only one threa will be allowed
	 * to enter in this method hence only one object will be created.
	 */
	static synchronized JBT createInstance() {
		if (instance == null){
instance = new JBT();
return instance;
}
		else
			return instance;
	}

	int i;
}
{{< /highlight>}}

##### Problem
The moment we use synchronized keyword it will create a problem for our multi-threaded application in terms of performance. So on one side, we are resolving the problem on another side we are creating one more problem. In the next approach, we will solve both this problem.

##### Implementation Three
{{< highlight java>}}
class JBT {

	/*
	 * This variable will be used to hold reference of JBT class.
	 * 
	 * Here we are creating the instance of JBT class and assigning the
	 * reference of that object to instance.
	 */
	private static JBT instance = new JBT();

	/*
	 * As private constructor is used so can not create object of this class
	 * directly. Except by using static method of same class.
	 */
	private JBT() {

	}

	/*
	 * This method will be used to get instance of JBT class. This method will
	 * check if there is already an object of class create or not if not then it
	 * will create an Object of JBT class and return the same else it will
	 * return the existing Object.
	 * 
	 * synchronized keyword is not required here.
	 */
	static JBT createInstance() {
		/*
		 *  As instance is already create and class loading time hence we can
		 *  directly return the same without creating any object.
		 */
		return instance;
	}

	int i;
}
{{< /highlight>}}

##### Problem
Here we are creating the object of JBT when class gets loaded. The object gets created even when it is not required. The object should be created only when it is required(Lazy Loading).  In the next approach, we will try to resolve this problem by using Double checking locking.

##### Implementation Four

{{< highlight java>}}
package com.jbt;

public class SingletonExample {

}

class JBT {

	/*
	 * This variable will be used to hold reference of JBT class.
	 * 
	 * Here we are creating the instance of JBT class and assigning the
	 * reference of that object to instance.
	 */
	private static JBT instance = null;

	/*
	 * As private constructor is used so can not create object of this class
	 * directly. Except by using static method of same class.
	 */
	private JBT() {

	}

	/*
	 * This method will be used to get instance of JBT class. This method will
	 * check if there is already an object of class create or not if not then it
	 * will create an Object of JBT class and return the same else it will return
	 * the existing Object.
	 * 
	 * Now block is marked as synchronized instead of whole method. So synchronized
	 * part will be used only once and that is when object is null. 
	 */
	static JBT createInstance() {
		if (instance == null)
		{
			synchronized(JBT.class){
				if (instance == null){
                                   instance = new JBT();
                                   return instance;
                             }
			}
		}

			return instance;
	}

	int i;
}
{{< /highlight>}}

##### Problem
All problem has been solved in this approach still synchronized keyword is used(Once) and that should be avoided.

##### Implementation Five (Initialization on Demand)

{{< highlight java>}}
class JBT {

	/*
	 * As private constructor is used so can not create object of this class
	 * directly. Except by using static method of same class.
	 */
	private JBT() {

	}

	/*
	 * Here static inner class is used instead of Static variable. It means
	 * Object will be lazy initialized.
	 */
	private static class LazyInit {
		private static final JBT instance = new JBT();
	}

	/*
	 * Whenever object JBT is required this method will be invoked and it will
	 * return the instance of JBT.
	 */
	static JBT createInstance() {
		return LazyInit.instance;
	}

	int i;
}
{{< /highlight>}}

##### Problem
What about Object creation using Clone and Serialization?? Next approach will handle that problem.

##### Implementation Six
To stop cloning of Object we will implement the Cloneable interface and throw CloneNotSupportedException. Also Serialized interface will be implemented and readObject will be used to return only one object at all time.

{{< highlight java>}}
class JBT implements Cloneable, Serializable{

	@Override
	protected Object clone() throws CloneNotSupportedException {
		return new CloneNotSupportedException();
	}

	protected Object readResolve() {
		return createInstance();
		}

	/*
	 * As private constructor is used so can not create object of this class
	 * directly. Except by using static method of same class.
	 */
	 private  JBT() {

	}

	/*
	 * Here static inner class is used instead of Static variable. It means
	 * Object will be lazy initialized.
	 */
	private static class LazyInit {
		private static final JBT instance = new JBT();
	}

	/*
	 * Whenever object JBT is required this method will be invoked and it will
	 * return the instance of JBT.
	 */
	static JBT createInstance() {
		return LazyInit.instance;
	}

	int i;
}
{{ /highlight}}

So this is the final implementation for singleton class. One more approach is there(ENUM). That I will discuss later.

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