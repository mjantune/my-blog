---
title:  "Git 8 - Modifying the Last Commit and Reverting"
categories: git reference
author: "Manuel"
toc: true
toc_sticky: true
---

### Changing The Last Commit

You've already made plenty of commits with the `git commit` command. Now with the `--amend` flag, you can alter the most-recent commit.

    $ git commit --amend

If your Working Directory is clean (meaning there aren't any uncommitted changes in the repository), then running `git commit --amend` will let you provide a new commit message. Your code editor will open up and display the original commit message. Just fix a misspelling or completely reword it! Then save it and close the editor to lock in the new commit message.

# Add Forgotten Files To Commit

Alternatively, `git commit --amend` will let you include files (or changes to files) you might've forgotten to include. Let's say you've updated the color of all navigation links across your entire website. You committed that change and thought you were done. But then you discovered that a special nav link buried deep on a page doesn't have the new color. You could just make a new commit that updates the color for that one link, but that would have two back-to-back commits that do practically the exact same thing (change link colors).

Instead, you can amend the last commit (the one that updated the color of all of the other links) to include this forgotten one. To do get the forgotten link included, just:

1. edit the file(s)
2. save the file(s)
3. stage the file(s)
4. and run `git commit --amend`

So you'd make changes to the necessary CSS and/or HTML files to get the forgotten link styled correctly, then you'd save all of the files that were modified, then you'd use `git add` to stage all of the modified files (just as if you were going to make a new commit!), but then you'd run `git commit --amend` to update the most-recent commit instead of creating a new one.

# What Is A Revert?

When you tell Git to **revert** a specific commit, Git takes the changes that were made in commit and does the exact opposite of them. Let's break that down a bit. If a character is added in commit A, if Git reverts commit A, then Git will make a new commit where that character is deleted. It also works the other way where if a character/line is removed, then reverting that commit will add that content back!

# The git revert Command

Now that I've made a commit with some changes, I can revert it with the git revert command

    $ git revert <SHA-of-commit-to-revert>

Since the SHA of the most-recent commit is `db7e87a`, to revert it: I'll just run `git revert db7e87a` (this will pop open my code editor to edit/accept the provided commit message)

I'll get the following output:

![Git log branches]( {{ site.baseurl }}/assets/ud123-l6-git-revert-post.png)

The Terminal application showing the output of reverting a commit. The output provides the commit message of the commit that was reverted. It also creates a new commit to record this change.

This command:

- will undo the changes that were made by the provided commit
- creates a new commit to record the change
