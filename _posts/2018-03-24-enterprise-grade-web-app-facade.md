---
layout: post
title:  "Enterprise grade web app facade"
date:   2018-03-24
categories: technology
permalink: /:categories/:title
comments: true
---

Over a period of time every software developer sees certain patterns/needs in terms of building and deploying apps which could be personal apps 
or enterprise grade. 

These patterns could be in terms of 
-   Design patterns - patterns that solve common recurring problems
-   performance engineering patterns - approach to evaluate the product in terms of performance - time and memory, bench marking and 
    validate against performance SLAs, profiling and identifying bottle necks
-   Logging standards, logging patterns, changing logging levels dynamically
-   Security - this is big, static and dynamic code analysis, ensure the app is covered against OWSAP top ten vulnerabilities like
    Sql injection, CSRF - cross site request forgery, XSS - Cross site scripting etc. Questioning on the need to store sensitive information
    like user credit card details, authentication information or using external services like OAuth for authentication. If storing sensitive 
    information what are some of the recommended ways to encrypt + salt + hash and store.
-   Persistence - What kind of persistence store does your service need. Sql ? NoSQL ? What kind of NoSql ?
-   UI - front end technologies like angular, extjs etc
-   Deployment landscape - what are the solutions that are out in the market for quickly and cost efficiently deploying your product.
    How to manage the dependencies for your app that is not baked into the app.
-   Containerization - Docker, why is this important to know ? How does this address deployment issues. Why is every major software vendor
    moving towards supporting containerization ?
-   AWS - again this is big. What can AWS do for your app ? Ease of deploying and maintaining the app.
-   Metrics for your app and its services
-   Revenue - Licensing model and marketing.


_There are certain things that are so common, like security, logging, service design, persistence, ui, metrics, revenue and so on in every app 
that you can create a FACADE._

What I want to offer :

**A FACADE - a skeleton per se, that embodies some of these commonality to give the service provider a predefined landscape, a predefined project 
that he/she can start from and focus on building the service they want to right from day 1 instead of worrying about researching and making decisions 
of what projects to choose from, what persistence to choose, how to handle security, how to deploy etc and etc**




