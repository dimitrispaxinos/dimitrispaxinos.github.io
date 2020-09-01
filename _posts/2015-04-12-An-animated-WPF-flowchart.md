---
layout: post
title: An animated WPF flowchart
tags: WPF XAML flowchart animation
---


### Introduction

There was recently a need to create an animated flowchart in order to depict the transition between the states of a workflow. This post presents the main points of the implementation. If you prefer to directly dive into the code,  you can find the complete implementation with a working sample on [**Github**](https://github.com/dimitrispaxinos/WPFDemos/tree/master/FlowChartDemo). The sample includes an animated flowchart for a blog post workflow like the one you can see below.
![](https://raw.githubusercontent.com/dimitrispaxinos/dimitrispaxinos.github.io/master/_assets/images/flowChartPostPic.gif)

### Implementation

The goal was to create a reusable component and therefore, the complete functionality is encapsulated in one user control, `FlowChartControl`, which has three dependency properties: 

 -  An `AvailableStatuses` dependency property of type *Type* which is an enum and contains all the available states of the workflow (You could also easily convert this to an `IEnumerable<string>` for example).
 - 	A `CurrentStatus` dependency property of type *Object* which represents the current status of the workflow.
 -	 An `Animate` dependency property of type *Bool* which is a flag that indicates whether the chart should animate or not.

<script src="https://gist.github.com/dimitrispaxinos/930979b71b7be156bab2.js"></script>

The `FlowChartControl` uses two subcontrols that represent the two geometric shapes available, `FlowChartCircle` and `FlowChartLine`. These controls include some triggers for defining the necessary color according to the state they are in and a `Content` dependency property for setting the state name. The code of these two controls is pretty straight forward and I will not get into the details of the implementation.

Let us focus on some interesting points of the FlowChartControl class instead.

<script src="https://gist.github.com/dimitrispaxinos/2753638b211bccdcf6a3.js"></script>

####   PropertyChangedCallback
All the action in this control resides in `CurrentStatusChangedCallBack()`  which is called every time the `CurrentStatus` dependency property is changed.

This method calls `CreateChart()`  which draws the flowchart, a StackPanel with horizontal orientation which we add the `FlowChartCircle` and `FlowChartLine` controls to.  

####  Animation
If the `Animate` dependency property is set to false, the opacity of the StackPanel is set to one and the complete flowchart becomes visible straight away. 

If set to true, the `CreateStoryBoard()` is called. This method sets the opacity of the flowchart to zero, iterates the StackPanel's children list and gradually increases the opacity from zero to one producing the desired animation. 
