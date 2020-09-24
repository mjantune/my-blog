---
layout: post
title:  "Git 9 - Resetting Commits"
categories: git reference
author: "Manuel"
---

# Reset vs Revert

At first glance, resetting might seem coincidentally close to reverting, but they are actually quite different. Reverting creates a new commit that reverts or undos a previous commit. Resetting, on the other hand, erases commits!

> ⚠️ Resetting Is Dangerous ⚠️

> You've got to be careful with Git's resetting capabilities. This is one of the few commands that lets you erase commits from the repository. If a commit is no longer in the repository, then its content is gone.

> To alleviate the stress a bit, Git does keep track of everything for about 30 days before it completely erases anything. To access this content, you'll need to use the git reflog command. Check out these links for more info:

    - [git-reflog](https://git-scm.com/docs/git-reflog)
    - [Rewriting History](https://www.atlassian.com/git/tutorials/rewriting-history)
    - [reflog, your safety net](http://gitready.com/intermediate/2009/02/09/reflog-your-safety-net.html)

# Relative Commit References

You already know that you can reference commits by their SHA, by tags, branches, and the special HEAD pointer. Sometimes that's not enough, though. There will be times when you'll want to reference a commit relative to another commit. For example, there will be times where you'll want to tell Git about the commit that's one before the current commit...or two before the current commit. There are special characters called "Ancestry References" that we can use to tell Git about these relative references. Those characters are:

- ^ – indicates the parent commit
- ~ – indicates the first parent commit

Here's how we can refer to previous commits:

- the parent commit – the following indicate the parent commit of the current commit
    - HEAD^
    - HEAD~
    - HEAD~1
- the grandparent commit – the following indicate the grandparent commit of the current commit
    - HEAD^^
    - HEAD~2
- the great-grandparent commit – the following indicate the great-grandparent commit of the current commit
    - HEAD^^^
    - HEAD~3

The main difference between the `^` and the `~` is when a commit is created from a merge. A merge commit has two parents. With a merge commit, the `^` reference is used to indicate the first parent of the commit while `^2` indicates the second parent. The first parent is the branch you were on when you ran git merge while the second parent is the branch that was merged in.

# The git reset Command

The git reset command is used to reset (erase) commits:

    $ git reset <reference-to-commit>

It can be used to:

- move the HEAD and current branch pointer to the referenced commit
- erase commits
- move committed changes to the staging index
- unstage committed changes

# Git Reset's Flags

The way that Git determines if it erases, stages previously committed changes, or unstages previously committed changes is by the flag that's used. The flags are:

*`--mixed`
*`--soft`
*`--hard`

It's easier to understand how they work with a little animation.

<iframe width="560" height="315" src="https://www.youtube.com/embed/UN7ki2G2yKc" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

# Reset Recap

To recap, the git reset command is used erase commits:

    $ git reset <reference-to-commit>

It can be used to:

- move the HEAD and current branch pointer to the referenced commit
- erase commits with the `--hard` flag
- moves committed changes to the staging index with the `--soft` flag
- unstages committed changes `--mixed` flag

Typically, ancestry references are used to indicate previous commits. The ancestry references are:

    `^` – indicates the parent commit
    `~` – indicates the first parent commit
