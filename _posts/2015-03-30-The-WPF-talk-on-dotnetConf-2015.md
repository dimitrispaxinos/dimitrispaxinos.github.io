---
layout: post
title: The WPF talk on dotnetConf 2015
tags: 
- WPF
- .NET
- dotnetConf2015

---

Following the recent posts on the [WPF Team blog](http://blogs.msdn.com/b/wpf/) after a long time of inactivity,  Microsoft continued its efforts to show that WPF development remains active by including  a [“WPF in 4.6 and beyond”](http://channel9.msdn.com/Events/dotnetConf/2015/WPF-in-46-and-beyond) talk on the [dotnetConf](http://www.dotnetconf.net/) 2015 that took place last week. This two day virtual conference included 19 talks in total which can be found on [Channel 9](http://channel9.msdn.com/Events/dotnetConf/2015).

The WPF talk provided an overview of the new WPF features that Microsoft is currently working on. Most of the changes and new features were already presented in the WPF Team blog earlier this year. The talk included live demonstration of these new capabilities using Visual Studio and Blend 2015.

Three were the most important features which were discussed with only one being presented for the first time during this talk. The first two were already known and are:

1. The new [UI Debugging tools](http://blogs.msdn.com/b/wpf/archive/2015/02/24/expanding-wpf-for-ui-debugging.aspx) that allow us to have access to the complete visual tree while debugging. This feature will integrate a functionality into Visual Studio 2015 that was until now provided by open source tools like [Snoop](https://snoopwpf.codeplex.com/). 
2. The [UI Performance Analysis Tool](http://blogs.msdn.com/b/wpf/archive/2015/01/16/new-ui-performance-analysis-tool-for-wpf-applications.aspx) which comes as a replacement for the XAML UI
Responsiveness tool which only worked for XAML based Windows Store applications. 

But the third and most important one was…

##WPF App Local

App Local shows Microsoft's clear intention to make WPF also take the vNext path.  This means that, in the near future, a WPF application will be possibly shipping with all the necessary WPF platform assemblies like PresentationFramework, PresentationCore, WindowsBase etc.

Instead of using the assemblies from the GAC, developers will be able to download a nuget package with all the above mentioned assemblies. 

This change will offer some very important advantages by:

 - Significantly improving performance according to Microsoft.
 - Allowing application developers to stop worrying about possible future versions’ incompatibility possibilities.
 - Giving the WPF team the ability to take a few more risks regarding future (a bit more radical) features without having to worry that much about any breaking changes.