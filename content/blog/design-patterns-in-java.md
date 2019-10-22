---
title: "Design Patterns in Java"
date: 2019-10-22T14:04:38+05:30
draft: false
tags: ["design, patterns"]
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

<p><a name="singleton"><h2>Singleton Design Pattern</h2></a></p>

### What is Singleton Design Pattern?

<p>If you are in Java then you must have used the new keyword. This new keyword creates an Object of class whenever required. But there are some scenarios where you don’t want to create individual Object for a different purpose. Singleton Pattern ensures that one and only one Object is instantiated for a given class. Whenever an object of a given class is required, only single(No more than one object) Object get returned.</p>

#### Implementation of Singleton Design Pattern

Now you know what is the Singleton Design Pattern. Next step would be to implement it. There are different ways you can implement Singleton. Before you start implementation, you need to understand what are the different ways to create an Object.

##### Different Ways to create an Object

<ul>
<li>'new' Keyword </li>
<li>Using 'the New Instance' (Reflection)</li>
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
{{< /highlight>}}

So this is the final implementation for singleton class. One more approach is there(ENUM). That I will discuss later.

<p><a name="factory"><h2>Factory Design Pattern</a></p>

### Why should I care?

<p style="text-align: justify;">Perhaps you have heard about programming to interfaces or just <em>not to program to implementations</em>. Every time you use the new keyword you create a <strong>concrete</strong> implementation of the given interface/abstract class/class. And this is bad.</p>

<p style="text-align: justify;"><em>Why is this bad?</em> You may ask. There is no problem with it theoretically, using new is the “only” way you can create a new object. At least until you find another way — but for now let’s stick with new. The only opponent of new is out a well-known friend in the IT: <strong>change</strong>.</p>
<p style="text-align: justify;">If we live the <em>best practice</em> of coding to interfaces we can make our application work with future implementations of this interface. As a basic example let’s write a simple method:</p>
<pre class="lang:java decode:true ">public void getFirst(List&lt;String&gt; input) {
   if(input != null &amp;&amp; !input.isEmpty())
       return input.get(0);
   return null;
}</pre>
<p style="text-align: justify;">Here we accept a List of String objects — the implementation does not matter. And List is an interface. We could naturally use ArrayList as expected parameter but this would limit some calls to our method. For example, someone has a LinkedList (which is a different implementation of List) and in this case, he/she has to convert all the elements into an ArrayList to call our method — so using List makes it more usable for others.</p>
<h2><span id="What_is_this_design_pattern_for">What is this design pattern for?</span></h2>
<p style="text-align: justify;">From the basic book of Design Patters (written by the so Called Gang of Four or GoF): “Defines an interface for creating an object, but lets subclasses decide which class to instantiate.”</p>
<p style="text-align: justify;">I would extend it with the following: a factory enables deferring the instantiation of subclasses.</p>
<h2><span id="Starting_with8230">Starting with…</span></h2>
<p>Let’s prepare our basic example where we can start.</p>
<p>We have a company which creates iOS applications. Our workflow looks like this:</p>
<pre class="lang:java decode:true">package hu.japy.dev.patterns;

/**
* This class contains the AppStore where we "create" iOS apps.
*
* @author GHajba
*
*/
public class AppStore {
   public void orderApp() {

       final App app = new App();

       app.develop();
       app.test();
       app.debug();
       app.deliver();
   }
}</pre><span id="ezoic-pub-ad-placeholder-110" class="ezoic-adpicker-ad"></span><span style='display:block !important;float:none;margin-bottom:15px !important;margin-left:0px !important;margin-right:0px !important;margin-top:15px !important;min-height:90px;min-width:728px;text-align:center !important;' class='ezoic-ad medrectangle-3 adtester-container adtester-container-110' data-ez-name='javabeginnerstutorial_com-medrectangle-3'><span id='div-gpt-ad-javabeginnerstutorial_com-medrectangle-3-0' ezaw='728' ezah='90' style='position:relative;z-index:0;display:inline-block;min-height:90px;min-width:728px;' class='ezoic-ad'><script data-cfasync='false' type='text/javascript' style='display:none;'>eval(ez_write_tag([[728,90],'javabeginnerstutorial_com-medrectangle-3','ezslot_3',110,'0','0']));</script></span></span>
<p style="text-align: justify;">Currently there is only one type of application we are creating, however what about the other Apple devices (iPhone / iPad, Apple Watch and Apple TV) we could create applications for?</p>
<p>We can add an enum to our orderApp method to distinguish between the different target machines:</p>
<pre class="lang:java decode:true">package hu.japy.dev.patterns;

/**
* Describes the available app types for our store.
*
* @author GHajba
*
*/
public enum AppType {
   IOS,
   WATCH,
   TV
}</pre>
<p style="text-align: justify;">In this case we need different implementations of the App class because every app has its own development / testing process. In this case we can either make the App class abstract or change it to an interface. I will use the abstract solution. As you know, the difference between the two approaches is that abstract classes can have default method-implementations which children can override (as with Java 8 interfaces can have one default method but they are limited to some point).</p>
<pre class="lang:java decode:true">public void orderApp(AppType type) {

   App app;
   switch (type) {
   case IOS:
       app = new IOSApp();
       break;
   case TV:
       app = new TVApp();
       break;
   case WATCH:
       app = new WatchApp();
       break;
   default:
       app = new IOSApp();
       break;
   }

   app.develop();
   app.test();
   app.debug();
   app.deliver();
}</pre><span id="ezoic-pub-ad-placeholder-113" class="ezoic-adpicker-ad"></span><span style='display:block !important;float:none;margin-bottom:15px !important;margin-left:0px !important;margin-right:0px !important;margin-top:15px !important;min-height:280px;min-width:336px;text-align:center !important;' class='ezoic-ad medrectangle-4 adtester-container adtester-container-113' data-ez-name='javabeginnerstutorial_com-medrectangle-4'><span id='div-gpt-ad-javabeginnerstutorial_com-medrectangle-4-0' ezaw='336' ezah='280' style='position:relative;z-index:0;display:inline-block;min-height:280px;min-width:336px;' class='ezoic-ad'><script data-cfasync='false' type='text/javascript' style='display:none;'>eval(ez_write_tag([[336,280],'javabeginnerstutorial_com-medrectangle-4','ezslot_4',113,'0','0']));</script></span></span>
<p style="text-align: justify;">This is fine until the already mentioned foe (change) comes along. For example Apple develops new gears and we want to stay in market so we create apps for them too, and some other products of Apple vanish with time. In this case we have to change our orderApp method again:</p>
<pre class="lang:java decode:true">public void orderApp(AppType type) {

   App app;
   switch (type) {
   case IOS:
       app = new IOSApp();
       break;
   case TV:
       app = new TVApp();
       break;
   case GLASS:
       app = new GlassApp();
       break;
   default:
       app = new GlassApp();
       break;
   }

   app.develop();
   app.test();
   app.debug();
   app.deliver();
}</pre>
<p style="text-align: justify;">As you can see, instantiating concrete implementations with new can really mess up our code — and you have to change this switch block is a new app type is provided and you have to know which class to instantiate.</p>
<h2><span id="Factory_Pattern_to_the_rescue">Factory Pattern to the rescue!</span></h2>
<p>However there is the Factory Pattern we can utilize and clean up this mess:</p>
<pre class="lang:java decode:true">package hu.japy.dev.patterns;

/**
* A simple Factory which encapsulates (hides) which concrete implementation to use for a given AppType.
*
* @author GHajba
*
*/
public class AppFactory {
   public App createApp(AppType type) {
       App app;
       switch (type) {
       case IOS:
           app = new IOSApp();
           break;
       case TV:
           app = new TVApp();
           break;
       case GLASS:
           app = new GlassApp();
           break;
       default:
           app = new GlassApp();
           break;
       }
       return app;
   }
}</pre>
<p style="text-align: justify;">This is basically to move the bunch of code of decision making into a separate class ending with Factory. It seems like some lazy thing but it is the real separation of concerns. You do not want to do how to instantiate an app of a given type — you only care to process the workflow. And this factory class comes to help.</p>
<p>Now we can re-write the orderApp method like this:</p>
<pre class="lang:java decode:true">public void orderApp(AppType type) {

   final App app = new AppFactory().createApp(type);

   app.develop();
   app.test();
   app.debug();
   app.deliver();
}</pre>
<p style="text-align: justify;">The given code is much clearer. In this case you only need to know that “There is an AppFactory which knows how to create apps of given types. Let’s get and use it!”.</p>
<p style="text-align: justify;">From now on you do not need to know what implementation of the App interface you need to create for a given type. It is all decided by the AppFactory class. It can happen, that two types result in the same application — but you do not have to do this and you can concentrate on the order to process.</p>
<h2><span id="Static_factories">Static factories</span></h2>
<p>Sometimes you can see factory classes which are static. This makes things easier because you do not need to instantiate a new version of the factory.</p>
<p>We could re-write our example factory above like this:</p>
<pre class="lang:java decode:true">public static App createApp(AppType type) {
   App app;
   switch (type) {
   case IOS:
       app = new IOSApp();
       break;
   case TV:
      app = new TVApp();
       break;
   case GLASS:
       app = new GlassApp();
       break;
   default:
       app = new GlassApp();
       break;
   }
   return app;
}</pre>
<p>Well, this is only a small change, adding a static modifier to the createApp method.<span id="ezoic-pub-ad-placeholder-118" class="ezoic-adpicker-ad"></span><span style='display:block !important;float:none;margin-bottom:15px !important;margin-left:0px !important;margin-right:0px !important;margin-top:15px !important;min-height:250px;min-width:300px;text-align:center !important;' class='ezoic-ad box-4 adtester-container adtester-container-118' data-ez-name='javabeginnerstutorial_com-box-4'><span id='div-gpt-ad-javabeginnerstutorial_com-box-4-0' ezaw='300' ezah='250' style='position:relative;z-index:0;display:inline-block;min-height:250px;min-width:300px;' class='ezoic-ad'><script data-cfasync='false' type='text/javascript' style='display:none;'>eval(ez_write_tag([[300,250],'javabeginnerstutorial_com-box-4','ezslot_7',118,'0','0']));</script></span></span></p>
<p>And then we can use it in the client like this:</p>
<pre class="lang:java decode:true">public void orderApp(AppType type) {

   final App app = AppFactory.createApp(type);

   app.develop();
   app.test();
   app.debug();
   app.deliver();
}</pre>
<p style="text-align: justify;">Beside this Java instantiates this Factory class only once when your application starts so you can use some functionality all along the application — for example a unique number generation — but this is out of the scope of this article.</p>
<h2><span id="Conclusion">Conclusion</span></h2>
<p style="text-align: justify;">Using the Factory Design Pattern fulfills the Separation of Concerns principle, leverages your knowledge of how to get the right version for a given interface or abstract class and as a side-effect, it makes your code clearer.</p>
<p style="text-align: justify;"><strong>However</strong> as with any of the Design Patterns do not start right away to use it in any case: make sure you can utilize all the functionality of the Design Pattern. If not it can make your code more complex and less readable!</p>



<p><a name="decorator"><h>Decorator design pattern in Java</h2></a></p>

<h2><span id="About_the_Decorator_Design_pattern">About the Decorator Design pattern</span></h2>
<p style="text-align: justify;">The concept of the decorator pattern is that it adds additional attributes to objects dynamically. This way you do not need to subclass the base to add extra functionality. This is good because with subclassing (extending) you change the behavior of all instances of the given class however you may only want some objects (instances of a given class) to change their behavior.</p>
<p style="text-align: justify;">The Gang of Four (GoF) book states the following about this pattern:</p>
<p style="text-align: justify;">Allows for the dynamic wrapping of objects in order to modify their existing responsibilities and behaviors.</p>
<h2><span id="When_to_use_the_pattern">When to use the pattern?</span></h2>
<p style="text-align: justify;">Knowing a pattern is good but as I mentioned earlier: use it with responsibility. Consider the following prior decorating everything in your Java project:</p>
<ul style="text-align: justify;">
<li>Should concrete implementations be decoupled from behaviors and responsibilities?</li>
<li>Should object responsibilities and behaviors be dynamically modifiable?</li>
</ul>
<p style="text-align: justify;">If you answer “Yes!” to the questions it may be a good idea to have subclasses but too many subclasses and too deep object-hierarchies are bad practice so you should avoid this.</p>
<h2><span id="How_to_use_Decorator_pattern">How to use Decorator pattern?</span></h2>
<p style="text-align: justify;">First of all you need a common denominator for your objects which you can extract to an interface. This gives the contract to all of the users that the implementations have a defined set of methods which can be called.</p>
<p style="text-align: justify;">Then you can create concrete implementors of this interface which are just normal citizens of your Java world.</p>
<p style="text-align: justify;">And you can create a decorator which implements this interface too <strong>and</strong> has an attribute of the same interface — the object which will be decorated with this behavior. And this decorator implementation (which can be an abstract class to extend its behavior of course) implements the contract-method of the interface and implements some extra behavior to the default implementation of the attribute’s.</p>
<p style="text-align: justify;">Seems complex? I bet with an example it will be very easy to understand.</p>
<h2><span id="Example">Example</span></h2>
<p>First of all let’s create the interface which gives us the contract:</p>
<pre class="lang:java decode:true">/**
 * Interface to create an app
 *
 * @author GHajba
 *
 */
public interface App {

    /**
     * This method creates an app for our app store. Seems silly and broken by design to have the App develop itself but
     * for this example it fits the purpose.
     */
    void developApp();
}

Now add a simple implementation of this interface which implements the contract method:

/**
 * @author GHajba
 *
 */
public class IOSApp implements App {

    @Override
    public void developApp() {
        System.out.println("Developing an iOS app");
    }
}</pre>
<p>We are all set and have an interface with an implementation so let’s try how it works:</p>
<pre class="lang:java decode:true">/**
 * This is the main entry point of the application
 *
 * @author GHajba
 *
 */
public class AppStore {

    public static void main(String... args) {
        final App app = new IOSApp();
        app.developApp();
    }
}</pre><span id="ezoic-pub-ad-placeholder-110" class="ezoic-adpicker-ad"></span><span style='display:block !important;float:none;margin-bottom:15px !important;margin-left:0px !important;margin-right:0px !important;margin-top:15px !important;min-height:90px;min-width:728px;text-align:center !important;' class='ezoic-ad medrectangle-3 adtester-container adtester-container-110' data-ez-name='javabeginnerstutorial_com-medrectangle-3'><span id='div-gpt-ad-javabeginnerstutorial_com-medrectangle-3-0' ezaw='728' ezah='90' style='position:relative;z-index:0;display:inline-block;min-height:90px;min-width:728px;' class='ezoic-ad'><script data-cfasync='false' type='text/javascript' style='display:none;'>eval(ez_write_tag([[728,90],'javabeginnerstutorial_com-medrectangle-3','ezslot_2',110,'0','0']));</script></span></span>
<p style="text-align: justify;">Running this application yields the following result:</p>
<p style="text-align: justify;">Developing an iOS app</p>
<p style="text-align: justify;">This is quite straightforward so let’s take the next step.</p>
<p style="text-align: justify;">We introduce the decorator. We make it for now abstract:</p>
<pre class="lang:java decode:true">/**
 * This is the basic implementation for our decorator. It is abstract so it does not need to implement the contract
 * method "developApp()".
 *
 * However it has the delegate which will be decorated later.
 *
 * @author GHajba
 *
 */
public abstract class AppDecorator implements App {
    /**
     * This is the delegate to decorate. It is package-private so the subclasses can access it so we do not need
     * getters/setters and a constructor. However I would add one if I would write this decorator in my daily job.
     */
    App delegate;
}</pre>
<p>And create two subclasses of this abstract Decorator to have interchangeable behavior:</p>
<pre class="lang:java decode:true">/**
 * This creates a decorated App with TV extension.
 *
 * @author GHajba
 *
 */
public class TVAppDecorator extends AppDecorator {

    /**
     * A required constructor to set the delegate for this app.
     *
     * @param delegate
     *            the delegate which should be decorated.
     */
    public TVAppDecorator(App delegate) {
        this.delegate = delegate;
    }

    @Override
    public void developApp() {
        this.delegate.developApp();
        System.out.println("Adding TV extension...");
    }
}

/**
 * This implementation of the decorator adds a Watch extension to the provided app.
 *
 * @author GHajba
 *
 */
public class WatchAppDecorator extends AppDecorator {

    /**
     * A required constructor to set the delegate for this app.
     *
     * @param delegate
     *            the delegate which should be decorated.
     */
    public WatchAppDecorator(App delegate) {
        this.delegate = delegate;
    }

    @Override
    public void developApp() {
        this.delegate.developApp();
        System.out.println("Adding Watch extension...");
    }
}</pre><span id="ezoic-pub-ad-placeholder-113" class="ezoic-adpicker-ad"></span><span style='display:block !important;float:none;margin-bottom:15px !important;margin-left:0px !important;margin-right:0px !important;margin-top:15px !important;min-height:280px;min-width:336px;text-align:center !important;' class='ezoic-ad medrectangle-4 adtester-container adtester-container-113' data-ez-name='javabeginnerstutorial_com-medrectangle-4'><span id='div-gpt-ad-javabeginnerstutorial_com-medrectangle-4-0' ezaw='336' ezah='280' style='position:relative;z-index:0;display:inline-block;min-height:280px;min-width:336px;' class='ezoic-ad'><script data-cfasync='false' type='text/javascript' style='display:none;'>eval(ez_write_tag([[336,280],'javabeginnerstutorial_com-medrectangle-4','ezslot_3',113,'0','0']));</script></span></span>
<p style="text-align: justify;">As you can see, the implementations of the decorator both implement the contract method a way different so let’s see what the application’s output is if we use these decorators:</p>
<pre class="lang:java decode:true">/**
 * This is the main entry point of the application
 *
 * @author GHajba
 *
 */
public class AppStore {

    public static void main(String... args) {
        final App tvApp = new TVAppDecorator(new IOSApp());
        tvApp.developApp();

        System.out.println("------");

        final App watchApp = new WatchAppDecorator(new IOSApp());
        watchApp.developApp();
    }
}</pre>
<p>Developing an iOS app<br>
Adding TV extension…<br>
——<br>
Developing an iOS app<br>
Adding Watch extension…</p>
<p>Naturally as I mentioned previously the decorator does not need to be an abstract class it can be a normal class too:</p>
<pre class="lang:java decode:true">/**
 * This is the decorator implementation which implements the decorator pattern by itself.
 *
 * @author GHajba
 *
 */
public class SimpleDecorator implements App {

    private final App delegate;

    /**
     * A required constructor to set the delegate for this app.
     *
     * @param delegate
     *            the delegate which should be decorated.
     */
    public SimpleDecorator(App delegate) {
        this.delegate = delegate;
    }

    @Override
    public void developApp() {
        System.out.println("Preparing extra content...");
        this.delegate.developApp();
        System.out.println("Fine-tuning the app to be more perfect...");
    }
}</pre>
<p>Now let’s see how this Decorator is used:</p>
<pre class="lang:java decode:true">/**
 * This is the main entry point of the application
 *
 * @author GHajba
 *
 */
public class AppStore {

    public static void main(String... args) {
        final App perfectApp = new SimpleDecorator(new IOSApp());
        perfectApp.developApp();
    }
}</pre>
<p>In this case the output would be the following:<span id="ezoic-pub-ad-placeholder-118" class="ezoic-adpicker-ad"></span><span style='display:block !important;float:none;margin-bottom:15px !important;margin-left:0px !important;margin-right:0px !important;margin-top:15px !important;min-height:250px;min-width:300px;text-align:center !important;' class='ezoic-ad box-4 adtester-container adtester-container-118' data-ez-name='javabeginnerstutorial_com-box-4'><span id='div-gpt-ad-javabeginnerstutorial_com-box-4-0' ezaw='300' ezah='250' style='position:relative;z-index:0;display:inline-block;min-height:250px;min-width:300px;' class='ezoic-ad'><script data-cfasync='false' type='text/javascript' style='display:none;'>eval(ez_write_tag([[300,250],'javabeginnerstutorial_com-box-4','ezslot_6',118,'0','0']));</script></span></span></p>
<p>Preparing extra content…<br>
Developing an iOS app<br>
Fine-tuning the app to be more perfect…</p>
<h2><span id="Conclusion">Conclusion</span></h2>
<p style="text-align: justify;">The Decorator Pattern is very useful in some cases but it has its downsides too. For example the Decorator and its enclosed components are not identical, this means that the instanceof comparison will fail in this particular case. So keep an eye open when you use this pattern!</p>


<p><a name="composite"><h2>Composite design pattern</h2></a></p>

<p style="text-align: justify;">Let’s see what the Gang of Four (GoF) tells us about this pattern:</p>
<p style="text-align: justify;">“Compose objects into tree structure to represent part-whole hierarchies. Composite lets client treat individual objects and compositions of objects uniformly.”</p>
<p style="text-align: justify;">In this pattern the client uses the component interface to interact with objects which are part of the composition. You can imagine the composite hierarchy as a tree where there are leaves and composites, and the requests are sent through this tree.</p>
<p style="text-align: justify;">If the recipient of the call is a leaf then the request is handled directly in this leaf. If the recipient is a composite then this composite forwards the requests to its children, alternatively this composite can perform additional operations before and after forwarding.</p>
<h2><span id="Example">Example</span></h2>
<p style="text-align: justify;">One good example for this pattern can be a company structure. For example the first entry point is the VP of Marketing who wants a new feature / software developed. So he (or she) calls up the VP of Software Development to implement this feature. The VP calls up the managers to give him a time/cost estimate. These managers forward this request to their managers or developers. When the responses get back they are returned until the VP of Software Development who answers the VP of Marketing.</p>
<p style="text-align: justify;">Let’s define the common interface of Employee. This interface defines the methods each employee of the company has to implement.</p>
<pre class="lang:java decode:true">/**
 * Interface to have a hierarchy of Employees.
 *
 * @author GHajba
 *
 */
public interface Employee {

    /**
     * @return the name of the employee
     */
    String getName();

    /**
     * @param e
     *            add this employee to the list of employees
     */
    void add(Employee e);

    /**
     * @param e
     *            remove this employee from the list of employees
     */
    void remove(Employee e);

    /**
     * @return the list of employees
     */
    List&lt;Employee&gt; getEmployees();

    /**
     * This method estimates the costs in ManDays for the given project. Managers delegate this request to their
     * employees, developers return an estimate.
     *
     * @param projectDescription
     * @return
     */
    int estimateProject(String projectDescription);
}</pre>
<p style="text-align: justify;">After this I created the hierarchy structure of the company: VP, SeniorManager. TeamLeader and Developer, where developers are the leaf nodes. To use more of the DRY (Don’t Repeat Yourself) principle I introduced a common Manager class which is abstract.</p>
<pre class="lang:java decode:true">/**
 * This abstract class implements the commmon functionality along all managers and gives them default methods which
 * "lazy" implementations do not have to cover.
 *
 * @author GHajba
 *
 */
public abstract class Manager implements Employee {
    List&lt;Employee&gt; employees = new ArrayList&lt;&gt;();
    String name;

    public Manager(String name) {
        this.name = name;
    }

    @Override
    public List&lt;Employee&gt; getEmployees() {
        return this.employees;
    }

    @Override
    public void add(Employee e) {
        if (e != null) {
            this.employees.add(e);
        }
    }

    @Override
    public void remove(Employee e) {
        if (e != null) {
            this.employees.remove(e);
        }
    }

    @Override
    public int estimateProject(String projectDescription) {
        if (this.employees.isEmpty()) {
            return 0;
        }
        return Math.round(this.employees.stream().mapToInt(e -&gt; {
            System.out.println(e);
            return e.estimateProject(projectDescription);
        }).sum() / this.employees.size());
    }

    @Override
    public String getName() {
        return this.name;
    }
}

/**
 * Simple implementation of a VP
 *
 * @author GHajba
 *
 */
public class VP extends Manager {

    public VP(String name) {
        super(name);
    }

    @Override
    public String toString() {
        return "I am " + getName() + ", VP";
    }

    /**
     * VP doubles the estimated amount.
     */
    @Override
    public int estimateProject(String projectDescription) {
        System.out.println("I am " + getName() + ", the VP, and calling for an estimate...");
        final int projectEstimate = super.estimateProject(projectDescription);
        System.out.println("Original estimate: " + projectEstimate);
        return Math.toIntExact(Math.round(projectEstimate * 2));
    }
}

/**
 * Simple implementation of a Senior Manager
 *
 * @author GHajba
 *
 */
public class SeniorManager extends Manager {

    public SeniorManager(String name) {
        super(name);
    }

    /**
     * Senior Managers add 10% to the estimate of the team.
     */
    @Override
    public int estimateProject(String projectDescription) {
        return Math.toIntExact(Math.round(super.estimateProject(projectDescription) * 1.1));
    }

    @Override
    public String toString() {
        return "I am " + getName() + ", Senior Manager";
    }
}

/**
 * Simple implementation of a Team Leader
 *
 * @author GHajba
 *
 */
public class TeamLeader extends Manager {

    public TeamLeader(String name) {
        super(name);
    }

    @Override
    public String toString() {
        return "I am " + getName() + ", Team Leader";
    }
}</pre><span id="ezoic-pub-ad-placeholder-110" class="ezoic-adpicker-ad"></span><span style='display:block !important;float:none;margin-bottom:15px !important;margin-left:0px !important;margin-right:0px !important;margin-top:15px !important;min-height:90px;min-width:728px;text-align:center !important;' class='ezoic-ad medrectangle-3 adtester-container adtester-container-110' data-ez-name='javabeginnerstutorial_com-medrectangle-3'><span id='div-gpt-ad-javabeginnerstutorial_com-medrectangle-3-0' ezaw='728' ezah='90' style='position:relative;z-index:0;display:inline-block;min-height:90px;min-width:728px;' class='ezoic-ad'><script data-cfasync='false' type='text/javascript' style='display:none;'>eval(ez_write_tag([[728,90],'javabeginnerstutorial_com-medrectangle-3','ezslot_2',110,'0','0']));</script></span></span>
<p style="text-align: justify;">As you can see, the Senior Managers and VPs implement their own version of the estimateProject method where they multiply the already estimated time by some factor. Team Leaders trust they developers.</p>
<p style="text-align: justify;">The Developer class has to implement some not relevant methods because they are Employees too. However because they are no managers they do not have employees so they cannot add or remove employees from their list — but they have to implement the estimateProject because developers are the leaves of this hierarchy.</p>
<pre class="lang:java decode:true">/**
 * Implementation of a plain-old Developer.
 *
 * @author GHajba
 *
 */
public class Developer implements Employee {

    String name;

    public Developer(String name) {
        this.name = name;
    }

    @Override
    public String getName() {
        return this.name;
    }

    @Override
    public void add(Employee e) {
    }

    @Override
    public void remove(Employee e) {
    }

    @Override
    public List&lt;Employee&gt; getEmployees() {
        return null;
    }

    @Override
    public int estimateProject(String projectDescription) {
        return new Random().nextInt(24);
    }

    @Override
    public String toString() {
        return "I am " + getName() + ", Developer";
    }
}

Now let's implement a structure and see how the pattern works:

/**
 * This is the main entry point of the application.
 *
 * @author GHajba
 *
 */
public class Composite {
    public static void main(String... args) {
        final Developer d1 = new Developer("Jack");
        final Developer d2 = new Developer("Jill");
        final Developer d3 = new Developer("Brian");
        final Developer d4 = new Developer("Bob");

        final Manager m1 = new TeamLeader("Marc");
        final Manager m2 = new TeamLeader("Christian");
        final Manager m3 = new TeamLeader("Phil");
        m1.add(d3);
        m1.add(d2);
        m2.add(d1);
        m3.add(d4);

        final Manager m4 = new SeniorManager("Harald");
        final Manager m5 = new SeniorManager("Klaus");

        m4.add(m3);
        m4.add(m2);
        m5.add(m1);

        final VP vp = new VP("Joseph");
        vp.add(m4);
        vp.add(m5);

        System.out.println("Our estimate is: " + vp.estimateProject("New exotic feature"));
    }
}</pre>
<p style="text-align: justify;">As you can see, this example requires <strong>Java 8</strong> at least because it utilizes the new <em>Stream API</em> and <em>lambdas</em>. And here is the result of a particular run:</p>
<p style="text-align: justify;">I am Joseph, the VP, and calling for an estimate…<br>
I am Harald, Senior Manager<br>
I am Phil, Team Leader<br>
I am Bob, Developer<br>
I am Christian, Team Leader<br>
I am Jack, Developer<br>
I am Klaus, Senior Manager<br>
I am Marc, Team Leader<br>
I am Brian, Developer<br>
I am Jill, Developer<br>
Original estimate: 9<br>
Our estimate is: 18</p>
<p style="text-align: justify;">This example output shows the tree structure where it starts with the VP and goes down for each node in the hierarchy. I could do some more fancy printing but I think you get the idea how this pattern works.</p>
<span id="ezoic-pub-ad-placeholder-113" class="ezoic-adpicker-ad"></span><span style='display:block !important;float:none;margin-bottom:15px !important;margin-left:0px !important;margin-right:0px !important;margin-top:15px !important;min-height:280px;min-width:336px;text-align:center !important;' class='ezoic-ad medrectangle-4 adtester-container adtester-container-113' data-ez-name='javabeginnerstutorial_com-medrectangle-4'><span id='div-gpt-ad-javabeginnerstutorial_com-medrectangle-4-0' ezaw='336' ezah='280' style='position:relative;z-index:0;display:inline-block;min-height:280px;min-width:336px;' class='ezoic-ad'><script data-cfasync='false' type='text/javascript' style='display:none;'>eval(ez_write_tag([[336,280],'javabeginnerstutorial_com-medrectangle-4','ezslot_3',113,'0','0']));</script></span></span><h2><span id="Disadvantages">Disadvantages?</span></h2>
<p style="text-align: justify;">When the tree-structure is defined the composite architecture makes the tree-structure general and this makes the leaf objects to have empty methods (or which just simply return nothing valuable) like the Developer class in the example.</p>
<h2><span id="Conclusion">Conclusion</span></h2>
<p style="text-align: justify;">This pattern can be used in situations when the problems represent a hierarchical relationship but they tend to have empty methods for leaf nodes in this hierarchy because of a common interface.</p>

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