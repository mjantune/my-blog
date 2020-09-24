---
layout: post
title:  "Git 5 - Add commits to a Repo"
categories: git reference
author: "Manuel"
---

# Git add

The git add command is used to move files from the Working Directory to the Staging Index.

    $ git add <file1> <file2> … <fileN>

This command:

- takes a space-separated list of file names
- alternatively, the period . can be used in place of a list of files to tell Git to add the current directory (and all nested files)

# Git Commit

To make a commit in Git you use the git commit command, but don't run it just yet. Running this command will open the code editor that you configured way back in the first lesson. If you haven't run this command yet:

    $ git config --global core.editor <your-editor's-config-went-here>

...go back to the Git configuration step and configure Git to use your chosen editor.

If you didn't do this step and you already ran git commit, then Git probably defaulted to using the "Vim" editor. Vim is a popular editor for people who have been using Unix or Linux systems forever, but it's not the friendliest for new users. It's definitely not in the scope of this course. Check out this [Stack Overflow post](https://stackoverflow.com/questions/11828270/how-to-exit-the-vim-editor) on how to get out of Vim and return to the regular command prompt.

If you did configure your editor, then go ahead and make a commit using the git commit command:

    $ git commit

Remember, your editor should pop open and you should see something like this:

![Git commit editor]( {{ site.baseurl }}/assets/ud123-l4-git-commit-editor.png)

# Git Commit Recap

The git commit command takes files from the Staging Index and saves them in the repository.

    $ git commit

This command:

- will open the code editor that is specified in your configuration
    (check out the Git configuration step from the first lesson to configure your editor)

Inside the code editor:

- a commit message must be supplied
- lines that start with a # are comments and will not be recorded
- save the file after adding a commit message
- close the editor to make the commit

Then, use `git log` to review the commit you just made!

# Git diff

**Why Do We Need This**

You might be like me where I start work on the next feature to my project at night, but then go to bed before I actually finish. Which means that, when I start working the next day, there are uncommitted changes. This is fine because I haven't finished the new feature, but I can't remember exactly what I've done since my last commit. git status will tell us what files have been changed, but not what those changes actually were.

The `git diff` command is used to find out this information!

The git diff command can be used to see changes that have been made but haven't been committed, yet.

    $ git diff

This command displays:

- the files that have been modified
- the location of the lines that have been added/removed
- the actual changes that have been made
