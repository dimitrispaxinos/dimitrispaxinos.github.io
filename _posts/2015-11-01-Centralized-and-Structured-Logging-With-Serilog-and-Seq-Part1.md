---
layout: post
title: Centralized & Structured .NET Logging with Serilog & Seq Part 1
tags: .NET serilog seq logging monitoring
---

### TL;DR
Serilog and Seq are two open-source tools that can help you introduce a centralized and structured logging mechanism in your .NET application really quickly. Has a quick learning curve and can substantially improve your logging, monitoring and error reporting workflow.

###  The Problem
The traditional approach of plain-text file based logging has some very important drawbacks. Log files have to be physically retrieved first and their contents have to subsequently be parsed into a structured form so that we can draw some useful conclusions. 

Retrieving the log file when dealing with a web application is not that hard you might say. What happens if you have a client-server application? How are you going to get the client log files? 

In the enterprise world, where LOB applications run in the intranet, the helpdesk could remotely connect to the computer where the client is running and retrieve the log file. But still... this could be better... 

### Serilog & Seq for the win

In this blog post, we are going to start examining a different logging approach which offers:

 >-  Structured meaningful logging objects
 >- A central repository for collecting these logs 
 >- A neat web interface with a queryable log list

using two open-source tools, Serilog and Seq. The goal is to get from reading to trying it out very fast. 

#### What is Serilog?
[Serilog](http://serilog.net/) is a logging .NET library like Log4Net which:

 - Logs structured event data. (complete JSON objects) 
 - Has a very clean and straightforward syntax. 
 - Can write the logs to many different places (the so-called [Sinks](https://github.com/serilog/serilog/wiki/Provided-Sinks)) like files, the console, DBs etc.

####    What is Seq?
[Seq](http://getseq.net/) is a complete solution for storing, displaying and querying structured event data which:

 - Can be installed in a matter of minutes
 - Works out of the box with Serilog
 - Has an API for the logs to be submitted
 - Has a web interface with a queryable log list
 - Has some other cool features like retention and event triggers.

### Let's try it out!

####    Installing Seq
1. Get Seq from [here](http://getseq.net/Download) and do a default install 
2. You can now access the web interface here: [http://localhost:5341/#/events](http://localhost:5341/#/events)

####    Serilog Basics

Fire up Visual Studio, create a console application and...

##### NuGet packages
Add the following two NuGet packages:

 - Serilog
 - Serilog.Sinks.Seq

##### Create Logger 
It is amazingly easy to create a logger that would write to our Seq server:
<script src="https://gist.github.com/dimitrispaxinos/f34abc870cf39a27e5de.js"></script>

##### Publish a log event - Log Event Levels
Publishing a log is as easy as using one line of code. You can use any of the following logging levels:
<script src="https://gist.github.com/dimitrispaxinos/b3571ae6f3f6b48156c9.js"></script>

And this is what you would see on the Seq web interface:

![](https://raw.githubusercontent.com/dimitrispaxinos/dimitrispaxinos.github.io/master/_assets/images/CentralizedStructuredLogging/SeqScreenShot_2.png)

##### Attaching Parameters
Let's now attach some parameters to our log event and make it a bit more meaningful:
<script src="https://gist.github.com/dimitrispaxinos/ed1b50385e3b71ec6d8d.js"></script>

The two parameters will be included in the logging event object as two additional properties with property names as declared in the log event string, `{FirstName}` and `{LastName}`:

![](https://raw.githubusercontent.com/dimitrispaxinos/dimitrispaxinos.github.io/master/_assets/images/CentralizedStructuredLogging/SeqScreenShot_3.png)

#####  Attaching Structured Objects
As said earlier, one of the strengths of Serilog is its ability to serialize and attach complete structured objects in its log event:
<script src="https://gist.github.com/dimitrispaxinos/7e0c9389e98a845b9938.js"></script>

As you can see below, you have to prefix your property name with '@' in order to be automatically serialized by Serilog:

![](https://raw.githubusercontent.com/dimitrispaxinos/dimitrispaxinos.github.io/master/_assets/images/CentralizedStructuredLogging/SeqScreenShot_4.png)

##### Attaching an Exception
Since we can attach stuctured objects, exceptions can also be attached:
<script src="https://gist.github.com/dimitrispaxinos/ba50c81dae503f17b905.js"></script>

and also highlighted in red within Seq:

![](https://raw.githubusercontent.com/dimitrispaxinos/dimitrispaxinos.github.io/master/_assets/images/CentralizedStructuredLogging/SeqScreenShot_5.PNG)

###  Summing up Part 1
In this first part, we went through the basics of using Serilog and Seq. The goal was to get you quickly up and running so that you can try it out yourself.  In Part 2, we will go through the contextual logging capabilities of Serilog, always in conjunction with Seq.

Continue with [Part2](http://www.dpaxinos.com/blog/2015/11/Centralized-and-Structured-Logging-With-Serilog-and-Seq-Part2/). 