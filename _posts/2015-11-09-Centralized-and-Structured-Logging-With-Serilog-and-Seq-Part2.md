---
layout: post
title: Centralized & Structured .NET Logging with Serilog & Seq Part 2
tags: .NET serilog seq logging monitoring
---


### Contextual Logging 
After [Part1](http://www.dpaxinos.com/blog/2015/11/Centralized-and-Structured-Logging-With-Serilog-and-Seq-Part1/) and the introduction to the basics of Serilog and Seq, we are now going to examine how we can add some context to our logging events. 

>When we say **Context**, we mean information that is implicitly added to the log event without including it in the actual log event submission.

Let's see how this works...

####Create Contextual Logger

In order to enable our Logger to 'carry' this context, we have to include the `.Enrich.FromLogContext()` part when we create it:

<script src="https://gist.github.com/dimitrispaxinos/789f7001592069ceae2c.js"></script>

####Add a property 
Let's add a property to the context using the static `PushProperty` method of the `LogContext` class that returns an `IDisposable`. As you can see, the context is only added to the call which is done within the using statement:

<script src="https://gist.github.com/dimitrispaxinos/4eaf3e0562bc3d731d9e.js"></script>

![](https://raw.githubusercontent.com/dimitrispaxinos/dimitrispaxinos.github.io/master/_assets/images/CentralizedStructuredLogging/SeqScreenShot_6.png)

####Add a structured object 
One of the biggest advantages of Serilog is also available for our context. Structured objects can also be included. We will use the `Person` class (like in Part 1) in order to create an object to be added to our context:

<script src="https://gist.github.com/dimitrispaxinos/83c6b01ef3122db63f6d.js"></script>

![](https://raw.githubusercontent.com/dimitrispaxinos/dimitrispaxinos.github.io/master/_assets/images/CentralizedStructuredLogging/SeqScreenShot_7.png)

####Add a dynamic object 
Dynamic objects can also be included. Imagine packing a number of properties into a dynamic object and adding this to your log event context:

<script src="https://gist.github.com/dimitrispaxinos/f466855297c2372d0400.js"></script>

![](https://raw.githubusercontent.com/dimitrispaxinos/dimitrispaxinos.github.io/master/_assets/images/CentralizedStructuredLogging/SeqScreenShot_8.png)

####Include the class name 
I think this is straightforward:
<script src="https://gist.github.com/dimitrispaxinos/3f8b01cc087eae37063f.js"></script>

We will get the same event in both cases with the class name being assigned to the `SourceContext` property:

![](https://raw.githubusercontent.com/dimitrispaxinos/dimitrispaxinos.github.io/master/_assets/images/CentralizedStructuredLogging/SeqScreenShot_9.png)

#### Add Context using Custom Enrichers

There is one more way to add context to your logs by using concrete classes in order to encapsulate the logic you would like to include. All you need to do is implement the `ILogEventEnricher` interface like in the following example:

<script src="https://gist.github.com/dimitrispaxinos/5192465d609f472ce502.js"></script>

You can then add your  `ILogEventEnricher`  to your context:

<script src="https://gist.github.com/dimitrispaxinos/a8f0133f6b9b185fa744.js"></script>

![](https://raw.githubusercontent.com/dimitrispaxinos/dimitrispaxinos.github.io/master/_assets/images/CentralizedStructuredLogging/SeqScreenShot_10.png)