---
# Page title
title: Development Collaboration

# Title for the menu link if you wish to use a shorter link title, otherwise remove this option.
linktitle: Collaboration

# Date page published
date: 2021-03-23

# Academic page type (do not modify).
type: book

# Position of this page in the menu. Remove this option to sort alphabetically.
weight: 3

draft: False

---

One of the most challenging aspects of software development is working effectively as part of a team. This problem is even more pronounced for ineperienced programmers because the way the code is organized will impact how well the team can collaborate. Fortunitly we are using Django, so the way our code will be organized has already been decided for us. Django projects are organized to take advantage of OOP and enable effective teamwork. What remains is how team members can share their work together and combine it into a single code base (or project).

There are two ways in which team members can collaborate or work together:

# 1- Syncronous Collaboration

In synchronous collaboration, the collaborating team members would all be online at the same time and work on the same file together. Such collaboration is easily enabled by replit.com and only requires that members share the link to the project they are working on. Replit.com does a good job of allowing teammembers to change the same file at the same time and communicate in realtime as they do so.

However, such collaboration has limitations:
1. Requires schedule coordination
2. Limited number of collaborators, ideally it makes sense to have 2 work together synchrousnly.
3. Contribution of members not tracked
4. Might require the availability of at least one experienced team member to succeed.

The main benefit of synchronous communication is **Knowledge Sharing**. The collaborators would work together on problem solving and the less experienced one would be learning greatly from the person they are collaborating with. Synchronous collaboration is similar is essence to eXprogramming.

# 2- Asynchronous Collaboration

In asynchronous collaboration, each member of the collaborating team would work on the project in their own time and do not need to interact directly with other team memebers. Instead, a system is used to manage how each memeber changes the code of the project and to enable the consolidation of work from multiple members into a single code base. This is by far the most effective and widely used method of collaboration in programming. Currently, the most popular system used to manage synchrnous collaboration is git, which is provided by github.com.

Using git, or github will require developers to learn a new tool that might not be easy to learn at first. But once the developers use the tool correctly, it is possible to enable the collaboration of thousands of developers on a single project, as can be seen in the [linux kernal project](https://github.com/torvalds/linux).

Fortunatly, replit.com integrates well with github. We will be using the main git features from within replite.com, and for other tasks such as merging  and resolving conflicts, we will use the web interface provided by github.com to perform these collaboration related tasks.

Using github is not suffecient for collaborating effectively. To be effective, the following conditions must be met:
1. Code organized to enable collaboration (Django forces that on the project in the way it organizes the code)
2. Team must agree on a workflow that describes how each member will start work, what to work on, and how to share it when done.
3. All team members must adhere to the workflow when coding for the project.

## Our Workflow

Each team will have their own workflow, and so we will be recommended a workflow for you to use in this course. The workflow is as follows:

1. When starting on a programming task, always create a new git branch for the task from the master branch. The branch would allow you to change the code for you only, and not affect the work of others. **NEVER work directly on the master branch**.
2. Ensure that the task you are working on is small and simple. If there are large and complex tasks, bread them down into smaller tasks.
3. Upon completion of the task, use github to send a pull request to merge the branch with the master branch.
4. It is the responsability of the project manager to respond to the pull request and merge it into the master branch.
5. Master branch should always have a working copy of the project, never a broken one.