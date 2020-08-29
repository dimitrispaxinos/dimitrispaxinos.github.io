---
layout: post
title: Binding an ItemsSource to an Enum
tags:  wpf xaml combobox tutorial 
description: fsdfsd
---

This rather quick post is about enabling an `Enum` to be set as the `ItemsSource` of a ComboBox, ListBox etc. You can find the sample code on [**Github**](https://github.com/dimitrispaxinos/WPFDemos/tree/master/EnumToItemSourceBindingSample). 

Our implementation will result in the following xaml code:

<script src="https://gist.github.com/dimitrispaxinos/01a5e62867ac8700cb2e.js"></script>

In the above code snippet, the ItemsSource is bound to the enum `Animals`

<script src="https://gist.github.com/dimitrispaxinos/7198401f09f9f7ba2c5b.js"></script>

by introducing a new MarkupExtension called `EnumToItemsSourceExtension`:

<script src="https://gist.github.com/dimitrispaxinos/42516a462fb2b6349646.js"></script>

By inheriting from the `MarkupExtension` class, we have to implement the abstract method `ProvideValue` .  Using the `Enum.GetValues()` method, we retrieve an array of the values of the constants in the provided enumeration (Animals) and we return it, so that the ItemsSource can bind to it.