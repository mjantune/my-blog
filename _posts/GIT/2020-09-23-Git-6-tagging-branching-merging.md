---
title:  "Git 6 - Tagging, Branching & Merging"
categories: git reference
author: "Manuel"
toc: true
toc_sticky: true
---

# Tagging

<iframe width="560" height="315" src="https://www.youtube.com/embed/D4VdXT72ASE" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

# Git Tag Command

Pay attention to what's shown (just the SHA and the commit message)

The command we'll be using to interact with the repository's tags is the git tag command:

    $ git tag -a v1.0

This will open your code editor and wait for you to supply a message for the tag. How about the message "Ready for content"?

>CAREFUL: In the command above (git tag -a v1.0) the -a flag is used. This flag tells Git to create an annotated flag. If you don't provide the flag (i.e. git tag v1.0) then it'll create what's called a lightweight tag.

>Annotated tags are recommended because they include a lot of extra information such as:

>- the person who made the tag
>- the date the tag was made
>- a message for the tag

> Because of this, you should always use annotated tags.

**Verify Tag**

After saving and quitting the editor, nothing is displayed on the command line. So how do we know that a tag was actually added to the project? If you type out just git tag, it will display all tags that are in the repository.

# Deleting A Tag

What if you accidentally misspelled something in the tag's message, or mistyped the actual tag name (v0.1 instead of v1.0). How could you fix this? The easiest way is just to delete the tag and make a new one.

A Git tag can be deleted with the -d flag (for delete!) and the name of the tag:

$ git tag -d v1.0

# Adding A Tag To A Past Commit

Running git tag -a v1.0 will tag the most recent commit. But what if you wanted to tag a commit that occurred farther back in the repo's history?

All you have to do is provide the SHA of the commit you want to tag!

    $ git tag -a v1.0 a87984

(after popping open a code editor to let you supply the tag's message) this command will tag the commit with the SHA a87084 with the tag v1.0. Using this technique, you can tag any commit in the entire git repository! 

# Branching

<iframe width="560" height="315" src="https://www.youtube.com/embed/ywcOC6CLG4s" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

The `git branch` command is used to interact with Git's branches:

    $ git branch

It can be used to:

- list all branch names in the repository
- create new branches
- delete branches

If we type out just `git branch` it will list out the branches in a repository:

# Create A Branch

To create a branch, all you have to do is use git branch and provide it the name of the branch you want it to create. So if you want a branch called "sidebar", you'd run this command:

    $ git branch sidebar