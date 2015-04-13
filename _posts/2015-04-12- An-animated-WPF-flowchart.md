---
layout: post
title: An animated WPF flowchart
tags: OData WebApi EntityFramework Unity Tutorial
---
##An animated WPF flowchart

###Introduction

There was recently a need to create an animated flowchart in order to depict the transition between the states of a workflow. The goal was to create a reusable component. You can find the code of the implementation on [**Github**](https://github.com/dimitrispaxinos/WPFDemos/tree/master/ProgressChartDemo). You can see a sample animated flowchart for a blog post workflow below.

PICTURE

###Implementation

In order to create a reusable component, the complete functionality is encapsulated in one user control, `ProgressChartControl`, which has three input parameters/dependency properties: 

 -  An `AvailableStatuses` dependency property of type *Type* which is an enum and contains all the available states of the workflow (You could also easily convert this to an `IEnumerable`).
 - 	A `CurrentStatus` dependency property of type *Object* which represents the current status of the workflow.
 -	 An `Animate` dependency property of type *Bool* which is a flag that indicates whether the chart should animate or not.

<script src="https://gist.github.com/dimitrispaxinos/930979b71b7be156bab2.js"></script>

`ProgressChartControl` comprises of two subcontrols that represent the two geometrical shapes available, `ProgressChartCircle` and `ProgressChartLine`. These controls include some triggers for defining the necessary color according to the state they belong to and a content dependency property for setting the state name. The code of these two controls is pretty straight forward and I will not get into the details of the implementation.

<script src="https://gist.github.com/dimitrispaxinos/2753638b211bccdcf6a3.js"></script>

Let us focus on some interesting points of the ProgressChartControl class.

Every time the CurrentStatus dependency property is changed, the method is called.
This method calls `CreateChart()`  which creates a list 

All the action in this control resides in `CurrentStatusCahnagedCallBack()`  which is called every time the Current Status dependency property is changed.

This method calls `CreateChart()`  which draws the flowchart, a StackPanel with horizontal orientation which we add the `ProgressChartCircle` and `ProgressChartLine` controls to.  

If the `Animate` dependency property is set to false, the opacity of the StackPanel is set to one and the complete flowchart becomes visible straight away. 

Otherwise, the `CreateStoryBoard()` method is called. It then sets the opacity of the flowchart to zero, iterates the StackPanel's children list and gradually increases the opacity from zero to one producing the desired animation. 
