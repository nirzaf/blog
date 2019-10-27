---
title: "Single Page Application With .Net Core and Blazor"
date: 2019-10-27T21:41:31+05:30
draft: false
tags : ["Blazor"]
---

!["Title Image"] (https://i.ibb.co/1f7yCMx/1-r8l-WHb-H-mg-Wkl462l-Qs-Yu-Q.jpg)

### Introduction
<p>In this article, we will create a Single Page Application (SPA) using server-side Blazor. We will use an Entity Framework Core database. Single-Page Applications are web applications that load a single HTML page. They dynamically update that page as the user interacts with the app.</p>

<P>We will be creating a sample Employee Record Management System. We will perform CRUD operations on it. A modal popup will display the form to handle user inputs. The form will also have a dropdown list which will bind to a database table. We will also provide a filter option to the user to filter the employee records based on employee name.</p>

<P>We will be using Visual Studio 2017 and SQL Server 2017 for our demo.</p>

<P>Let us look at the final application:</p>

!["Final Application"](https://i.ibb.co/ChT6Fwj/1-w4-PSdj1u-M9j-MFx4-N-fulw.gif)

### What is Server-Side Blazor?

<P>The release 0.5.0 of Blazor allows us to run Blazor applications on the server. This means that we can run the Blazor component server-side on .NET Core. A SignalR connection over the network will handle other functionalities such as UI updates, event handling, and JavaScript interop calls.</p>

### Prerequisites

<ul>
<li>Install the .NET Core 2.1 or above SDK from <a href="https://dotnet.microsoft.com/learn/dotnet/hello-world-tutorial/intro#windowscmd">here</a></li>
<li>Install Visual Studio 2017 v15.7 or above</li>
<li>Install ASP.NET Core Blazor Language Services extension from <a href="https://marketplace.visualstudio.com/items?itemName=aspnet.blazor">here</a></li>
<li>SQL Server 2012 or above.</li>
</ul>

<P>Visual Studio 2017 versions below v15.7 do not support the Blazor framework.</p>

### Source Code

<P>Get the source code for this application from <a href="https://github.com/nirzaf/Blazor-Server-Side-SPA">Github<a>/</p>

##### Important Note :

<P>This article is valid for Blazor 0.5.0 release. The server-side Blazor might undergo breaking changes in future releases of Blazor.</p>

##### Creating a Table

<P>We will be using two tables to store our data.</p>
<ol>
<li><p>Employee: Used to store employee details. It contains fields such as EmployeeID, Name, City, Department, and Gender.</p></li>
<li><p>Cities: This contains the list of cities. It is used to populate the City field of the Employee table. It contains two fields, CityID and CityName</P></li>
</ol>

<P>Execute the following commands to create both tables:</p>

{{< highlight SQL>}}
CREATE TABLE Employee (  
EmployeeID int IDENTITY(1,1) PRIMARY KEY,  
Name varchar(20) NOT NULL ,  
City varchar(20) NOT NULL ,  
Department varchar(20) NOT NULL ,  
Gender varchar(6) NOT NULL  
)    
GO      
      
CREATE TABLE Cities (      
CityID int IDENTITY(1,1) NOT NULL PRIMARY KEY,      
CityName varchar(20) NOT NULL       
)      
GO
{{< /highlight>}}

<P>Now, we will put some data into the Cities table. We will be using this table to bind a dropdown list in our web application. The user will select the desired city from this dropdown. Use the following insert statements:</p>

{{< highlight SQL >}}
INSERT INTO Cities VALUES('New Delhi');  
INSERT INTO Cities VALUES('Mumbai');  
INSERT INTO Cities VALUES('Hyderabad');  
INSERT INTO Cities VALUES('Chennai');  
INSERT INTO Cities VALUES('Bengaluru');
{{< /highlight>}}

<P>Now, our Database part is complete. So we will proceed to create the server side application using Visual Studio 2017.</p>

### Create The Server Side Blazor Application

<P>Open Visual Studio and select File >> New >> Project.</p>

<P>After selecting the project, a “New Project” dialog will open. Select .NET Core inside the Visual C# menu from the left panel. Then, select “ASP.NET Core Web Application” from the available project types. For project name, put in ServerSideSPA and press OK.</p>
<P></p>
<P></p>
<P></p>
<P></p>
<P></p>

