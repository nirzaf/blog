---
title: "Angular Interview Questions and Answers Part 1"
date: 2019-09-21T09:59:03+05:30
draft: false
---
!["Angular Logo"](https://res.cloudinary.com/dw0ygv1p9/image/upload/v1571632021/1_klTLGz5T5Ryy4QVBkgsNCQ_lf5kdf.jpg)

### Q1. What is Angular 4 and how it differs from Angular 1.x?

Angular 4 is a Javascript framework built around the concept of components, and more precisely, with the Web Components standard in mind. It was rewritten from scratch by the Angular team using Typescript (although we can use it with ES5, ES6, or Dart as well).

<p>Angular 4 is a big change for us compared to 1.x. Because it is a completely different framework than 1.x, and is not backward-compatible. Angular 4 is written entirely in Typescript and meets the ECMAScript 6 specification. The main differences are:</p>

<ul>
    <li>
         Angular 4 is entirely component based. Controllers and $scope are no longer used. They have been replaced by components and directives.
    </li>
    <li>
    Angular 4 uses TypeScript. TypeScript will not be used in the browser directly. So the program code is compiled to JavaScript. This can be achieved with “Traceur”.
    </li>
    <li>
    The digest cycle from Angular 1.x has been replaced by another internal mechanism known as “Change Detection”. This feature, along with other improvements and tweaks, yields a considerable increase in performance.
    </li>
    <li>
    Unlike Angular 1.x where we can get most of the functionalities in angular.js file, Angular 4 follows module pattern. We need to import the functions ourself and export them when we need anywhere else.
    </li>
    <li>
    There are no more factory, service, provider in Angular 4. We need to use class for declaring a service.
    </li>
</ul>

## Q2. What is component decorators in Angular 4?

The main objectives of decorators is to add some metadata to the class that will tell Angular 4 how to process a class. Or in another words, Decorators are functions that modify JavaScript classes. Angular has many decorators that attach metadata to classes so that it knows what those classes mean and how they should work.

<p>
If we consider Component in Angular 4, we will have following options to configure.
</p>


<ul>
    <li>
         <strong>selector:</strong> — define the name of the HTML element in which our component will live.
    </li>
    <li>
    <strong>Template or templateUrl</strong>: — It can be inline string or link an external html file. It allows us to tie logic from our component directly to a view.
    </li>
    <li>
    <strong>styles: </strong>— the styles array for our specific component. We can also link external CSS by styleUrls.
    </li>
    <li>
    <strong>directives:</strong> — another component directives we want to use inside our components.
    </li>
    <li>
    <strong>providers: </strong>— This is the place we are passing the services that we need insider our components.
    </li>
</ul>

Immediately after this decorator or right to it, we need to export a class where our variables and functions reside that our component uses.

{{< highlight typescript>}}
  export class sampleComponent{
      name:'Angular 4';
  }
{{< /highlight>}}

### Q3. What is compilation in Angular 4? And what are the types of compilation in Angular 4?

<p>An Angular application consists largely of components and their HTML templates. Before the browser can render the application, the components and templates must be converted to executable JavaScript by the Angular compiler.</p>

<p>
There is actually only one Angular compiler. The difference between AOT and JIT is a matter of timing and tooling. There are two types of compilation Angular 4 provides.
</p>

<ul>
    <li>
    <strong>Just-in-time (JIT) compilation:</strong> This is a standard development approach which compiles our Typescript and html files in the browser at runtime, as the application loads. It is great but has disadvantages. Views take longer to render because of the in-browser compilation step. App size increases as it contains angular compiler and other library code that won’t actually need.
    </li>
    <li>
       <strong> Ahead-of-time (AOT) compilation:</strong> With AOT, the compiler runs at the build time and the browser downloads only the pre compiled version of the application. The browser loads executable code so it can render the application immediately, without waiting to compile the app first. This compilation is better than JIT because of Fast rendering, smaller application size, security and detect template errors earlier.
    </li>
</ul>

### Q4. What is @NgModule?

An NgModule class describes how the application parts fit together. Every application has at least one NgModule, the root module that we bootstrap to launch the application.

{{< highlight typescript>}}
import {NgModule} from '@angular/core';
import {BrowserModule} from '@angular/platform-browser';
import {AppComponent} from './app.component';

@NgModule({
    imports : [BrowserModule],
    declarations: [AppComponent],
    bootstrap: [AppComponent]
})

export class AppModule{}
{{< /highlight>}}

Here the AppComponent is the root module of our application that Angular creates and inserts it into the index.html page.

### Q5. What are all the metadata properties of NgModule? And what are they used for?

<em>`@NgModule`</em> accepts a metadata object that tells Angular how to compile and launch the application. The properties are:

<ul>
    <li>
    imports – Modules that the application needs or depends on to run like, the BrowserModule that every application needs to run in a browser.
    </li>
    <li>
    declarations – the application's components, which belongs to the NgModuleclass. We must declare every component in an `NgModule` class. If we use a component without declaring it, we'll see a clear error message in the browser console.
    </li>
    <li>
    bootstrap – the root component that Angular creates and inserts into the index.html host web page. The application will be launched by creating the components listed in this array.
    </li>
</ul>

### Q6. What is Template reference variables?

A template reference variable (#var) is a reference to a DOM element within a template. We use hash symbol (#) to declare a reference variable in a template

{{< highlight javascript>}}
<input #name placeholder="Your Name"> 
{{name.value}}
{{< / highlight>}}

<p>
In the above code the #name declares a variable on the input element. Here the name refers to the input element. Now we can access any property of the inputDOM, using this reference variable. For example, we can get the value of the inputelement as name.value and the value of the placeholder property by name.placeholder anywhere in the template.
</p>
<p>
Finally, a Template reference variable refers to its attached element, component or directive. It can be accessed anywhere in the entire template. We can also use ref- instead of #. Thus we can also write the above code as ref-name.
</p>

##### Some more set of questions will be posted in next part