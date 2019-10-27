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

!["Create New Project"](https://i.ibb.co/d4V4txw/1-8-Eh0-Zv9u-Aln49u5yq-GGv-AA.png)

<P>After selecting the project, a “New Project” dialog will open. Select .NET Core inside the Visual C# menu from the left panel. Then, select “ASP.NET Core Web Application” from the available project types. For project name, put in ServerSideSPA and press OK.</p>

!["Create Blazor Pages"](https://i.ibb.co/XjrwcxH/1-cb-ZGSKGs-HLOt-Po-Nkjk7-WSQ.png
)
<P>This will create our server-side Blazor solution. You can observe the folder structure in solution explorer, as shown in the below image:</p>

!["Solution Explorer"](https://i.ibb.co/wpwsCJk/1-9b6-Xh-Oy-B7-MMP0n-Ou-RCym-A.png)

#### The solution has two project files:

<ol>
<li><p>ServerSideSPA.App: This is our server-side Blazor app. This project has all our component logic and our services. We will also create our models and data access layer in this project.</p></li>
<li><p>ServerSideSPA.Server: This is the ASP.NET Core hosted application. Instead of running client-side in the browser, the server-side Blazor app will run in the ASP.NET Core host application.</p></li>
</ol>

<P>In future releases of Blazor, these two projects might be merged into one. But for now, the separation is required due to the differences in the Blazor compilation model.</p>

### Scaffolding the Model to the Application

<P>We are using Entity Framework core database first approach to create our models. We will create our model class in ServerSideSPA.App project.
Navigate to Tools >> NuGet Package Manager >> Package Manager Console. Select “ServerSideSPA.App” from the Default project drop-down. Refer to the image below:</p>

!["Scafolding"](https://i.ibb.co/qpTrVjW/1-3-Aj-B-3k-AOuv-Zs4-K9kb-DCDg.png)

<P>First, we will install the package for the database provider that we are targeting which is SQL Server in this case. Hence, run the following command:</p>

{{< highlight SQL >}} Install-Package Microsoft.EntityFrameworkCore.SqlServer {{< /highlight>}}

<P>Since we are using Entity Framework Tools to create a model from the existing database, we will install the tools package as well. Hence, run the following command:</p>

{{< highlight SQL >}} Install-Package Microsoft.EntityFrameworkCore.Tools {{< /highlight>}}

<P>After you have installed both packages, we will scaffold our model from the database tables using the following command:</p>

{{< highlight SQL >}} Scaffold-DbContext "Your connection string here" Microsoft.EntityFrameworkCore.SqlServer -OutputDir Models -Tables Employee, Cities {{< /highlight>}}

<P>Do not forget to put your own connection string (inside “ ”). After this command executes successfully, it creates a models folder inside ServerSideSPA.App project. It contains three class files: myTestDBContext.cs, Cities.cs and Employee.cs. Hence, we have successfully scaffolded our Models using EF core database first approach.</p>

### Creating the Data Access Layer for the Application

<p>Right-click on ServerSideSPA.App project and then select Add >> New Folder and name the folder DataAccess. We will be adding our class to handle database related operations inside this folder only.</p>

{{< highlight SQL >}} {{< /highlight>}}

<P></p>
<P></p>
<P></p>
<P></p>
<P></p>
<P></p>
<P></p>
<P></p>
<P></p>
<P></p>
<P></p>
<P></p>
<P></p>
<P></p>

