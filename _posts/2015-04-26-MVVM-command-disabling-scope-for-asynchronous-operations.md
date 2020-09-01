---
layout: post
title: MVVM Command disabling scope for asynchronous operations
tags: MVVM C# WPF async Command
---


### Introduction

One of the must-have features of all modern applications is constant UI responsiveness. The user interface should never freeze and stay responsive no matter what service calls or other background operations are being executed. So, when there is an operation running in the background, the user should only be able to take certain actions that do not interfere with the running operation.  Two common approaches to tackling this problem would be:

1. Blocking the UI completely while displaying a loading animation with a message. 
2. Disabling only the actions (buttons for example) that the user is not allowed to take while the operation is in progress. 

In this post, we will go through a possible implementation for the second case. You can also find a full working sample of the implementation that follows on **[Github](https://github.com/dimitrispaxinos/WPFDemos/tree/master/AsyncDisablingScopeSample)**. We will start by defining the disabling scope of an operation. 

####  Disabling Scope
Let's suppose that we have a contacts list (like the one you can see below) in which we can add a new or update/remove the selected contact (in red). When someone adds a contact by clicking the add button, a time consuming background task is executed (service call). While this task is being executed, the Update and Remove buttons should be disabled. Therefore, these two buttons would be the **disabling scope** of the Add Button action.

![Disabling Scope](https://raw.githubusercontent.com/dimitrispaxinos/dimitrispaxinos.github.io/master/_assets/images/mvvmAsyncCommandScope_OriginalFormWithScope.jpg)


### Implementation
If you are familiar with the MVVM pattern, then you have definitely already made use of Commands and the `ICommand` Interface. There are various implementations of this interface. A popular one, suitable for asynchronous operations is the [RelayCommandAsync](https://gist.github.com/dimitrispaxinos/f051d67a287bb34947a5).

The constructor of this implementation looks like this:

<script src="https://gist.github.com/dimitrispaxinos/cb0912bd4c132e0e9fca.js"></script>

####  The Initial Approach

We can define the Command Handler and set the conditions under which the Command should be enabled.
An initial approach could look like this:

<script src="https://gist.github.com/dimitrispaxinos/68fd37a522ab0b39f613.js"></script>

The `RemoveCommand` can execute when the selected contact is not null and the `AddCommand` is not executing. The `AddCommandHandler` changes accordingly the boolean `IsAddCommandExecuting`  which enables or disables the `RemoveCommand` .

The ViewModel condition `SelectedContact!= null` is a responsibility of the Command itself. The same could happen with the Disabling scope as well though. When looking at the `AddCommand` declaration, you cannot directly see the disabling scope of the Command. 

####  One step further
What if we introduced a new `IDisableable`  interface, a new `DisablingScope` class and finally an `IDisableableCommand` interface:

<script src="https://gist.github.com/dimitrispaxinos/4a5a27b7bcbd9d2edfa8.js"></script>

After these last changes, the `IsAddCommandExecuting` is not necessary anymore and the `AddCommandHandler` would now look like this: 

<script src="https://gist.github.com/dimitrispaxinos/ef2f232e281910042318.js"></script>

####  Polishing up
Now, we can directly see which buttons belong to the disabling scope of the Command by looking at the Command Handler. What if we could improve this a little bit more and make it more clear. We could perhaps skip the `using` part every time a handler is called. What if we encapsulated this functionality in the `RelayCommandAsync` class? Then, we have the following `IDisableableCommand` implementation:

<script src="https://gist.github.com/dimitrispaxinos/e3a9ed7d9560b2a8a837.js"></script>

After these last changes, the`AddCommand` declaration would be:

<script src="https://gist.github.com/dimitrispaxinos/edc847c6d03238d08db7.js"></script>

As you can see, it becomes absolutely clear which Commands are being disabled while the `AddCommand` is executing and all that without any affecting the `AddCommandHandler`.