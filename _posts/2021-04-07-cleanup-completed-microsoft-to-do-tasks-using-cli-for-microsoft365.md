---
layout:         post
title:          Clean up completed Microsoft To Do tasks using CLI for Microsoft 365
category:       CLI for Microsoft 365
tags:           [CLI,Microsoft 365,To Do,Tasks]
permalink:      /:year/:month/:title
---

Microsoft To Do is my task management tool of choice, I use it for tracking everything I do, which means I generate and complete a lot of tasks during a working week.

So why have I written a script to delete completed tasks, they just get hidden right? 

One of the things that I wish would be better is the search capability in Microsoft To Do. I use the Microsoft To Do iOS app for managing my tasks and task lists, using keywords on tasks so that I can search on a keyword and return tasks containing that keyword which don't all reside in the same task list.

Unfortunately, the search does not provide any filters and returns all tasks containing the keyword including those that have been completed, this makes it hard to see at a glance the active tasks that I have against that keyword.

Using the CLI for Microsoft 365 however we can easily solve this issue, as I am not concerned about tasks that I have completed, I have written a script that iterates across all of the task lists and removes the tasks that have been marked as completed.

<script src="https://gist.github.com/garrytrinder/17f58a45693dae1a44fde2bacb86461a.js"></script>

> CLI for Microsoft 365 is associated with the [Microsoft 365 Patterns and Practices](https://pnp.github.io) (PnP) organisation, which is a virtual team consisting of Microsoft employees and community members focused on helping the community make the best use of Microsoft products.