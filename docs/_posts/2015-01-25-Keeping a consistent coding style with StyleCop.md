---
layout: post
title: Keeping a consistent coding style with StyleCop
tags: StyleCop CodingStyle VisualStudio
description: A post about the use of StyleCop to ensure that your coding style remains consistent.
---

### Coding Style and its Importance

According to [Wikipedia](http://en.wikipedia.org/wiki/Programming_style) , programming or coding style *"is a set of rules or guidelines used when writing the source code for a computer program"*.  Well factored code with consistent style provides your projects and your team with additional value. The code has a standard structure which makes it easily readable and reduces the time needed by new or existing developers in your team to understand your code.

### What is StyleCop and why should I use it?

Within a team, people usually agree on a common writing style coming up with some rules that have to be followed by all team members. This is where [StyleCop](https://stylecop.codeplex.com/) comes to rescue since it is an open source project of Microsoft which, as stated on the project’s website, *“analyzes C# source code to enforce a set of style and consistency rules”.* StyleCop can be run either locally on every computer from inside Visual Studio or centrally when integrated with your CI server. 

### StyleCop Rules
The installation of StyleCop is straightforward. Once installed, you can go to the installation folder and open the *Settings.StyleCop* file. All StyleCop rules are located in this file. StyleCop ships with a default configuration file which can be easily modified through its configuration editor as you can see in the picture below.

![StyleCop Settings](https://raw.githubusercontent.com/dimitrispaxinos/dimitrispaxinos.github.io/master/_assets/images/StyleCopSettings.png)

### Visual Studio
Once you install StyleCop, you can start using it from within Visual Studio. You can check your code at solution, project or file level by executing the "Run StyleCop" command in every context menu. Code that does not conform with the StyleCop rules is underlined and the tooltip informs us about the exact rule which is violated providing also the rule's Id as you can see below. You can find the rule in the configuration file of StyleCop by entering the rule's Id in the "Find" text box in the upper right corner of the configuration editor.

![StyleCop Settings](https://raw.githubusercontent.com/dimitrispaxinos/dimitrispaxinos.github.io/master/_assets/images/StyleCopSnippet.png)


### Multiple Configuration Files
When StyleCop runs, it first looks for a settings file in the same folder where the .cs file is and then starts going up the folders until it finds the next available configuration file. This offers a great flexibility since you can have different configuration files at project, solution or machine level.

### MSBuild
It is also possible to run all StyleCop checks at every build and see the violations as warnings in your output window. This has to be configured at project level and can be done in two ways, either by [modifying your project file](https://stylecop.codeplex.com/wikipage?title=Setting%20Up%20StyleCop%20MSBuild%20Integration) or by referencing the StyleCop.Msbuild NuGet package. And if you are absolutely serious about it, there is also another option that enables to treat StyleCop violations as build errors.

### Continuous Integration Server
As mentioned above, you can integrate StyleCop with the CI server of your choice. The technical aspect of this goes beyond the scope of this post. Despite that, here are two good tutorials for [TFS](http://www.towfeek.se/2014/05/customize-your-tfs-build-process-to-run-stylecop/) and [TeamCity](http://www.andyfrench.info/2014/06/integrating-stylecop-with-teamcity.html). 