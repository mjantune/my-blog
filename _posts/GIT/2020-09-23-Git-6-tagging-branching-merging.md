---
layout: post
title:  "Git 6 - Tagging and Branching"
categories: git reference
author: "Manuel"
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

To create a branch, all you have to do is use `git branch` and provide it the name of the branch you want it to create. So if you want a branch called "sidebar", you'd run this command:

    $ git branch sidebar

# The git checkout Command

Remember that when a commit is made that it will be added to the current branch. So even though we created the new sidebar, no new commits will be added to it since we haven't switched to it, yet. If we made a commit right now, that commit would be added to the master branch, not the sidebar branch. We've already seen this in the demo, but to switch between branches, we need to use Git's checkout command.

    $ git checkout sidebar

It's important to understand how this command works. Running this command will:

- remove all files and directories from the Working Directory that Git is tracking
    - (files that Git tracks are stored in the repository, so nothing is lost)
- go into the repository and pull out all of the files and directories of the commit that the branch points to

So this will remove all of the files that are referenced by commits in the master branch. It will replace them with the files that are referenced by the commits in the sidebar branch. This is very important to understand, so go back and read these last two sentences.

The funny thing, though, is that both `sidebar` and `master` are pointing at the same commit, so it will look like nothing changes when you switch between them. But the command prompt will show "sidebar", now:

# Branches In The Log

The branch information in the command prompt is helpful, but the clearest way to see it is by looking at the output of git log. But just like we had to use the --decorate flag to display Git tags, we need it to display branches.

    $ git log --oneline --decorate

This is what my log output displays (yours might look different depending on what commits you've made):

![Git log branches]( {{ site.baseurl }}/assets/ud123-l5-git-log-branches.png)

# Delete A Branch

A branch is used to do development or make a fix to the project that won't affect the project (since the changes are made on a branch). Once you make the change on the branch, you can combine that branch into the master branch (this "combining of branches" is called "merging" and we'll look at it shortly).

Now after a branch's changes have been merged, you probably won't need the branch anymore. If you want to delete the branch, you'd use the -d flag. The command below includes the -d flag which tells Git to delete the provided branch (in this case, the "sidebar" branch).

    $ git branch -d sidebar

One thing to note is that you can't delete a branch that you're currently on. So to delete the sidebar branch, you'd have to switch to either the master branch or create and switch to a new branch.

Deleting something can be quite nerve-wracking. Don't worry, though. Git won't let you delete a branch if it has commits on it that aren't on any other branch (meaning the commits are unique to the branch that's about to be deleted). If you created the sidebar branch, added commits to it, and then tried to delete it with the `git branch -d sidebar`, Git wouldn't let you delete the branch because you can't delete a branch that you're currently on. If you switched to the master branch and tried to delete the sidebar branch, Git also wouldn't let you do that because those new commits on the sidebar branch would be lost! To force deletion, you need to use a capital D flag - `git branch -D sidebar`.

# Git Branch Recap

To recap, the `git branch` command is used to manage branches in Git:

{% highlight bash %}
# to list all branches
$ git branch

# to create a new "footer-fix" branch
$ git branch footer-fix

# to delete the "footer-fix" branch
$ git branch -d footer-fix
{% endhighlight %}

This command is used to:

- list out local branches
- create new branches
- remove branches


>💡 Switch and Create Branch In One Command💡

>The way we currently work with branches is to create a branch with the git branch command and then switch to that newly created branch with the `git checkout` command.
>But did you know that the git checkout command can actually create a new branch, too? If you provide the -b flag, you can create a branch and switch to it all in one command.

    $ git checkout -b richards-branch-for-awesome-changes

> It's a pretty useful command, and I use it often.

