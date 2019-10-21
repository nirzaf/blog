---
title: "How Not to Get 30k Bill From Firebase"
date: 2019-09-15T11:56:47+05:30
draft: false
tags: ["firebase"]
---

!["How not to get $30k Bill From Firebase"](https://res.cloudinary.com/dw0ygv1p9/image/upload/v1571639382/1_Oow_RBnaByCoR57FO1kbKw_ne8ah8.png)

July last year, a crowd funding campaign went viral in Colombia. It was all good and dandy in the first 48 hours. They managed to reach over 2 million sessions and over 20 million page views — with a website that stayed fully functional without a hitch.
<strong>Until they saw the bill.</strong>

$30,356.56USD in 72 hours.
<p>
Whatever gains they had in the crowdfunding campaign would soon be eaten up by the cost of running the application.</p>

## Why did it go so wrong?

One of the biggest differences between Firebase and traditional cloud based databases is the pricing model. Amazon, Digital Ocean, Google Cloud, Microsoft Azure and all other providers uses a pay per hour model for instance based databases.

<p>Firebase, however, charges based on per 100k — 250k read, write and delete requests to the database. If you can keep it within this range, then your actual bill shouldn’t cost more than $25. Amazon’s DynamoDB works on a similar pricing mantra, except they split the data storage cost from the read and write requests.</p>
<p>In contrast, traditional cloud databases are limited by the number of concurrent connections available at each tier and it doesn’t really matter what or how much you interact with your database since it’s already being paid for by the hour. Any caveats to this is in each individual service and its provider’s fine print.</p>
<p>The Colombian crowdfunding campaign made the mistake of reading every document entry in a certain collection in order to calculate the total collected and support values each time a user looked at a particular view. This meant that if there were 100 donations, the application would make a call to the database once but the actual act of reading would equate to 100 reads twice — once for the values required to calculate the total and second time for the number of supporters — totaling 200 read request.</p>
<p>Things got worse when this number is required to be displayed on multiple pages and therefore calculated several times. When the number of supporters started to hit the thousands and page views climbed to more than 2 million, it became very easy for read requests to the database to reach billions.</p>
<p>This isn’t a Google billing error or the tech giant trying grab money. This is a case of human error in a data structure not optimized for efficiency. The Colombian startup would have faced database connections maxed out issues or something similar even if they went with a traditional cloud hosted solution instead of Firebase. The root of the issue is in the number of connections and data transferred — not the service itself.</p>

## How to keep things under $25

<p>When we use Firebase, we tend to only think about the database aspect of the service. However, Google provides a generous amount of cloud function invocations with the package. One could almost say they they are trying to encourage us to use it.</p>
<p>With 2 million invocations per month or $0.40 per million on the pay as you go pricing model, it makes you wonder why they would give out so much in comparison to read/write/delete interactions to the database.</p>
<p>With Firebase being a tableless structure, it’s easy to boot up aggregate tables for data request optimization. Not only is it faster to return results, the number of read/write/delete requests also goes down significantly.</p>
<p>The crowdfunding campaign used a data structure in Firebase that is similar to the diagram illustrated below.</p>

<img src="https://res.cloudinary.com/dw0ygv1p9/image/upload/v1571639838/1_ndOz2mZKKLLHDzM20UwC6Q_yenzok.jpg" title="">

<p>However, the above structure is inefficient for scaling even though the actual infrastructure has the capabilities of handling it.</p>
<p>Cloud functions act as a cheap micro service back end that cuts down process that occurs on the front end. In the diagram below, when a payment document is inserted into the collection, it triggers a cloud function that updates another document in a collection that is keeping track of data that needs to be calculated. As a result, the first trigger results in three actions — two document writes and one read. While this may feel like more read and writes, most applications are read heavy and thus needs to be optimized for it.</p>

<img src="https://res.cloudinary.com/dw0ygv1p9/image/upload/v1571639961/1_oHvnS_l69P2G-5xwosbOHA_nrcedm.jpg" alt="">
<p>With this structure, it means that when data is requested, only data in campaign 1 is required, resulting in a single read instead of returning five separate results.
When this structure scales up to one million views, you’re only expected to make one million read calls rather than explode exponentially as more payments are made. It can get worse if your app updates in real time.</p>

## Rethinking the way you write your apps

<p>It doesn’t really matter if you’re with Firebase or not. Hosting apps nowadays is cheap but databases in general can still be costly if not kept in check. Data is what makes an application and the connections, read and write requests are the things that happen the most when it comes to the traffic flow between different parts of the application.</p>

<p>While the front end is quick to boot up, the backend is what keeps everything organized and in check. Traditional architectures offers data sessions in the backend but serverless architectures often don’t have this benefit.</p>
<p>However, more space and processing power is required to run the backend which can beef up your overall bill. Serverless structures offers an on-demand kind of service which can end up costing less. Thinking about how your data will continue to persist will impact on the speed of response and number of total reads and writes required to give you the data you need. The less processing required after, the better it is for your overall application’s cost scalability over time.</p>







