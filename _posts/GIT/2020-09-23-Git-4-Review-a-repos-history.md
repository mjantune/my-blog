---
title:  "Git 4 - Review a Repo's History"
categories: git reference
author: "Manuel"
toc: true
toc_sticky: true
---

#The Git Log Command

Finding the answers to these questions is exactly what git log can do for us! Instead of explaining everything that it can do for us, let's experience it! Go ahead and run the git log command in the terminal:

    $ git log

The terminal should display the following screen.

[The Git Log output]({{ site.baseurl }}/assets/ud123-l3-git-log-output.png)

Navigating The Log

If you're not used to a pager on the command line, navigating in Less can be a bit odd. Here are some helpful keys:  

- to scroll down, press
    - `j` or ↓ to move down one line at a time
    - `d` to move by half the page screen
    - `f` to move by a whole page screen
- to scroll up, press
    - `k` or ↑ to move _up_ one line at a time
    - `u` to move by half the page screen
    - `b` to move by a whole page screen
press `q` to quit out of the log (returns to the regular command prompt)
  
Git records a ton of information when a commit is made. See if you can use git log to answer the following questions!

# Changing How Git Log Displays Information

We've been looking closely at all the detailed information that git log displays. But now, take a step back and look at all of the information as a whole.

Let's think about some of these questions:

- **the SHA** - git log will display the complete SHA for every single commit. Each SHA is unique, so we don't really need to see the entire SHA. We could get by perfectly fine with knowing just the first 6-8 characters. Wouldn't it be great if we could save some space and show just the first 5 or so characters of the SHA?
- **the author** - the git log output displays the commit author for every single commit! It could be different for other repositories that have multiple people collaborating together, but for this one, there's only one person making all of the commits, so the commit author will be identical for all of them. Do we need to see the author for each one? What if we wanted to hide that information?
- **the date** - By default, git log will display the date for each commit. But do we really care about the commit's date? Knowing the date might be important occasionally, but typically knowing the date isn't vitally important and can be ignored in a lot of cases. Is there a way we could hide that to save space?
- **the commit message** - this is one of the most important parts of a commit message...we usually always want to see this

What could we do here to not waste a lot of space and make the output smaller? We can use a flag.

# git log --oneline

The git log command has a flag that can be used to alter how it displays the repository's information. That flag is --oneline:

    $ git log --oneline

This command:

- lists one commit per line
- shows the first 7 characters of the commit's SHA
- shows the commit's message

# Viewing Modified Files
We just looked at the --oneline flag to show one commit per line. That's great for getting an overview of the repository. But what if we want to dig in a little to see what file or files were changed by a commit?

# git log --stat Intro

The `git log` command has a flag that can be used to display the files that have been changed in the commit, as well as the number of lines that have been added or deleted. The flag is `--stat` ("stat" is short for "statistics"):

    $ git log --stat

[The Git Log Stat]({{ site.baseurl }}/assets/ud123-l3-git-log-vs-git-log-stat.png)
Two Terminal applications side-by-side. The left one shows the result of the git log command with all of the information while the right one shows the result of the git log --stat command which lists the files that were changed as well as the number of added/removed lines.

This command:

- displays the file(s) that have been modified
- displays the number of lines that have been added/removed
- displays a summary line with the total number of modified files and lines that have been added/removed

# Viewing File Changes

git log -p

The git log command has a flag that can be used to display the actual changes made to a file. The flag is --patch which can be shortened to just -p:

    $ git log -p

# New Command: git show

The other command that shows a specific commit is git show:

    $ git show

Running it like the example above will only display the most recent commit. Typically, a SHA is provided as a final argument:

    $ git show fdf5493

What does git show do?

The git show command will show only one commit. So don't get alarmed when you can't find any other commits - it only shows one. The output of the git show command is exactly the same as the git log -p command. So by default, git show displays:

- the commit
- the author
- the date
- the commit message
- the patch information

However, git show can be combined with most of the other flags we've looked at:

* `--stat` - to show the how many files were changed and the number of lines that were added/removed
* `-p` or `--patch` - this the default, but if --stat is used, the patch won't display, so pass -p to add it again
* `-w` - to ignore changes to whitespace

