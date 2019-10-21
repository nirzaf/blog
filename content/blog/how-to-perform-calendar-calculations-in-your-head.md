---
title: "How to perform calendar calculations in your head"
date: 2019-09-20T13:13:01+05:30
draft: false
image: "https://res.cloudinary.com/dw0ygv1p9/image/upload/v1571614434/calculator_te6ik2.png"
tags: ["logical-thinking"]
comments: false
---
![so-called calendrical savant (or calendar savant) is](https://res.cloudinary.com/dw0ygv1p9/image/upload/v1571614434/calculator_te6ik2.png)
so-called calendrical savant (or calendar savant) is someone who despite their intellectual disability (typically autism) can name the day of the week of a given date, or visa versa in a few seconds or even a tenth of a second (Kennedy & Squire, 2007). In the clip below, mega-savant Kim Peek, inspiration for the movie Rain Man, does so while taking questions from an audience:

![GraphQL Growth](https://res.cloudinary.com/dw0ygv1p9/image/upload/v1571615348/pexels-photo-209224.jpeg_h7ukmt.jpg)

While extremely impressive to behold, calendar calculations are actually very simple to perform and can be learned in less than 30 minutes. This short article will teach you how.

{{< youtube k2T45r5G3kA >}}

## What day was the 13th of January 1989

My birthday. I was born two weeks late. Here is how to calculate which day of the week that was (Lancaster, 2005)

### Step 1. Calculate the Year Code Y

The first step of our five step process is to calculate the year code, represented by the letter Y. This is done in the following way:

{{< highlight html >}}
Calculate the Year Code Y
Take the last two digits of the year, divide by 4, remove the remainder. For my birthday, 89 / 4 = 22. Add the number to the last two digits of the year, 22 + 89 = 111
For dates in the 1700s, add 4.
For dates in the 1800s, add 2.
For dates in the 1900s, add 0.
For dates in the 2000s, add 6.
For dates in the 2100s, add 4.
{{< /highlight >}}

So, for the date 13th of January 1989 we obtain the year code Y =111.

### Step 2. Find the Month Code M\

The second step of our five step calculation is to find the month code M. This is a simple step, simply look it up in the table below (or better, memorize it):

{{< highlight html>}}

Month        Code
January      1*
February     4*
March        4
April        0
May          2
June         5
July         0
August       3
September    6
October      1
November     4
December     6
If the year you are calculating for is/was a leap year, subtract 1 from the code for January and February, so January = 0 and February = 3.

{{</highlight>}}

As we know, leap years occur every four years (even years). Century years like 1900, 2000 and 2100 are leap years if they are evenly divisible by 400.
For the date 13th of January 1989, we obtain the month code M = 1.

### Step 3. Find the Day Code D

The third step of our five step calculation is to find the day code D. This iS even easier than finding the month code, as it is simply the number of the date itself. For the 13th of January 1989, the number is D = 13.

### Step 4. Find the sum of the numbers Y + M + D

The fourth step of our five step model is to add the three numbers we’ve found. For our three numbers, the sum is 111 + 1 + 13 = 125.

### Step 5. Find the Day of the week

The final step of the calculation is to calculate the remainder of the modulo operation 125 mod 7. We know that 7 x 17 is 119, leaving a remainder of 6:

{{< highlight go >}}
Day         Remainder
Saturday    0
Sunday      1
Monday      2
Tuesday     3
Wednesday   4
Thursday    5
Friday      6
{{</highlight>}}

The 13th of January 1989 was a Friday. Yes, I was born on Friday the 13th
