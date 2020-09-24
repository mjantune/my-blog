---
layout: post
title:  "Git 3 - Determine a Repo's Status"
categories: git reference
author: "Manuel"
---

Working with Git on the command line can be a little bit challenging because it's a little bit like a black box. I mean, how do you know when you should or shouldn't run certain Git commands? Is Git ready for me to run a command yet? What if I run a command but I think it didn't work...how can I find that out? The answer to all of these questions is the git status command!

    $ git status

## Git Status Output

The git status command will display a lot of information depending on the state of your files, the working directory, and the repository. You don't need to worry too much about these, though...just run git status and it will display the information you need to know.

![Git Status GIF]({{ site.baseurl }}/assets/ud123-l2-git-status-blog-project.gif)

# Git Status Recap

The git status command will display the current status of the repository.

$ git status

I can't stress enough how important it is to use this command all the time as you're first learning Git. This command will:

    tell us about new files that have been created in the Working Directory that Git hasn't started tracking, yet
    files that Git is tracking that have been modified
    a whole bunch of other things that we'll be learning about throughout the rest of the course ;-)
