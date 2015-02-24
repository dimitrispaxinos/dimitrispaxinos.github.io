---
layout: post
title: Rewriting history with Git
tags: 
- Git
- Version Control
- Productivity
- Rebase
- Merge
- Squash
---
How many times have you wished you could…

- Change or add something in the code you just committed? 
- Merge small commits in your project history?
- Keep all commits of a feature branch when transferring your code changes to the main branch?

Well, with Git, all the above is actually possible. Git has been around for a while and there is enough online information regarding its main advantages over centralized version control systems (CVCS). I would like to focus on three not-so-well advertised features that I consider real game changers. 

---

**Caution: You should never try to rewrite any public history. The following Git functionalities are only meant to be used with your local commits and not any commits already pushed to the central repository.**

---

### A Git Workflow in an agile environment
Before proceeding to these cool Git features, let's talk about a possible Git workflow first. On agile software development projects, work is organized in user stories which define the features to be developed. Since branching in Git is very easy and cheap, one approach would be to have one master/dev branch and create further branches for every user story/feature. This has the benefit of each feature being separately developed without interfering with any others. When the feature is ready, it gets integrated into the main branch.

###Modify your last commit with Git amend

I do not know about you but this keeps happening to me quite often; realizing, shortly after committing, that there is something I would like to change in my commit. With Git, all we have to do is make our changes and just type:

    git commit --amend 
This way, we include the new changes in our most recent commit while keeping the original commit message. In case we also want to change the message we just type:

    git commit --amend -m "New commit message"

###Squashing your commits with interactive rebase
Generally, being able to commit any intermediate changes made before completing a task is very useful, especially when trying different approaches in order to solve a problem. This can also be done using a CVCS, but the project history ends up including many small or meaningless commits. 

This can be easily solved with Git and its *interactive rebase*  feature which gives us the opportunity to reorganize the existing commits by squashing different consequent commits into a single one. This results in having a neat project history, with most of our changes grouped together. Such an approach would also allow for much easier code reviews since the code is organized in logical units-commits.  

####Interactive Rebase Example
Let's go through a simple example. Imagine having a branch with four commits. In our example, we would like to squash the fourth into the third commit.

![Squash](https://raw.githubusercontent.com/dimitrispaxinos/dimitrispaxinos.github.io/master/_assets/images/GitSquash1.png)

In order to be able to edit the last three commits, we type:

    git rebase -i head~3

and then we are asked to choose the commits to be squashed:

![Squash](https://raw.githubusercontent.com/dimitrispaxinos/dimitrispaxinos.github.io/master/_assets/images/GitSquash2.png)

We replace "pick" with "squash" for the fourth commit:

![Squash](https://raw.githubusercontent.com/dimitrispaxinos/dimitrispaxinos.github.io/master/_assets/images/GitSquash3.png)

In order to save the changes and exit the VI editor, we escape and type `:wq`.  After this step, we also have the opportunity to modify our commit messages:

![Squash](https://raw.githubusercontent.com/dimitrispaxinos/dimitrispaxinos.github.io/master/_assets/images/GitSquash4.png)

After replacing the message of the third commit (the fourth one will be included in the third commit), the squash takes place as expected and our branch history finally looks like this:

![Squash](https://raw.githubusercontent.com/dimitrispaxinos/dimitrispaxinos.github.io/master/_assets/images/GitSquash5.png)


###Rebase instead of merge

Imagine creating a new branch in order to start working on a new feature according to the Git workflow we talked about earlier. While working on your secondary branch, there are some changes made on the master branch by other members of our team.

![StyleCop Settings](https://raw.githubusercontent.com/dimitrispaxinos/dimitrispaxinos.github.io/master/_assets/images/GitTwoBranches.PNG)

After finishing our feature, we want to transfer the changes from the secondary to the master branch. The obvious choice would normally be to merge the changes. This would create a new single commit on our master branch with the changes of the secondary branch.

![StyleCop Settings](https://raw.githubusercontent.com/dimitrispaxinos/dimitrispaxinos.github.io/master/_assets/images/GitMerge.png)

But what if we could directly transfer our neat commits (that we could also clean up using interactive rebase as described above) to your main branch? Git can do that by rebasing instead of merging. Rebasing actually means reapplying the commits of the secondary branch on your master branch starting after the last commit on the master branch.

![StyleCop Settings](https://raw.githubusercontent.com/dimitrispaxinos/dimitrispaxinos.github.io/master/_assets/images/GitRebase.png)

This option can contribute to keeping a very clean project history while retaining all steps towards developing your new feature. 

####Rebase Example

Let's now have a look at an example to make it more clear. We will continue working on the example we started a while ago for showing the interactive rebase feature. We were working on the master branch and now, we will create one more branch for a feature 

    git branch featureBranch
    git checkout featureBranch

where we will do two more commits. The history would then look like this:
 
![Rebase](https://raw.githubusercontent.com/dimitrispaxinos/dimitrispaxinos.github.io/master/_assets/images/GitRebaseCmd1.png)

If we now return to our master branch 

    git checkout master

and do another two commits there as well, its history will look like this:

![Rebase](https://raw.githubusercontent.com/dimitrispaxinos/dimitrispaxinos.github.io/master/_assets/images/GitRebaseCmd2.png)

We will transfer our changes from our feature branch now by reapplying the commits one by one on top of our last commit on the master branch.

    git rebase featureBranch

After rebasing, the history of the master branch will be looking like this:

![Rebase](https://raw.githubusercontent.com/dimitrispaxinos/dimitrispaxinos.github.io/master/_assets/images/GitRebaseCmd4.png)
