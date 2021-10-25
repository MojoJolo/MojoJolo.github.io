---
layout: post
title: "If not fixed, our code will fail every Sunday"
date: 2021-10-25
description: Sunday is represented in different numbers in Java / Scala compared to C#. Apparently, it is also different in Python.
---

Last night, I was just checking our email alerts before I go to sleep, I noticed that there are high number of errors in one of our backend services. Weirdly enough, it started at exactly 12am.

When I checked the logs, I noticed that the issue was caused by one of our methods that deals with time. It puzzled me for a while since that feature was running smoothly for almost a week now. We also had tests that covers it. Upon further investigation, I realized that...

**Sundays are different in Scala.**

To provide a bit of context, this part of our backend code that deal with dates was migrated from C# to Scala. This backend code also uses a config file that have dates represented as numbers. Sunday is 0, Monday is 1... Saturday is 7. We did it this way to follow how C# deals with days of week.

Our mistake is that we didn't know that day of week is represented differently in different programming languages.

- For C#, **Sunday is 0**, Monday is 1, and Saturday is 6. Here's the [documentation](https://docs.microsoft.com/en-us/dotnet/api/system.dayofweek?view=net-5.0).
- For Java (hence Scala), **Sunday is 7**, Monday is 1, and Saturday is 6. Here's the [documentation](https://docs.microsoft.com/en-us/dotnet/api/system.dayofweek?view=net-5.0). It's not 0 based, and week starts at Mondays.
- I also checked for Python and [it's also different](https://docs.python.org/3/library/datetime.html#datetime.datetime.weekday). The default is that Monday is 0, Saturday is 5, and **Sunday is 6**.

In these three programming languages, Sundays are represented in three different numbers.

*Moral of the story: We need to write better test cases.*

I don't have much to tell anymore, <sub>but I feel that weeks should start on Sundays, right?</sub>
