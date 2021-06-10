# Basic Git Commands

## init

Create an empty local git repo.
Syntax: `git init`

## clone

Clone some remote repo onto our computer
Syntax: `git clone <repo-git> <new-name-for-repo>`

Documentation page: [This is the docs page](https://git-scm.com/book/en/v2/Git-Basics-Getting-a-Git-Repository#Cloning-an-Existing-Repository)

## status

Know the status of the git repo
Syntax: `git status`

**Example** :

_On branch master
Your branch is up-to-date with 'origin/master'.
nothing to commit, working directory clean_

The output tells us two things:

1. On branch master – this tells us that Git is on the master branch. You've got a description of a branch on your terms sheet so this is the "master" branch (which is the default branch). We'll be looking more at branches in lesson 5

2. Your branch is up-to-date with 'origin/master'. – Because git clone was used to copy this repository from another computer, this is telling us if our project is in sync with the one we copied from. We won't be dealing with the project on the other computer, so this line can be ignored.nothing to commit, working directory clean – this is saying that there are no pending changes.

## log

Shows the history of all git commits made in the past along with commit msg, time and author
Syntax: `git log`

Use arrow keys to navigate.

To see only the commit messages and SHA instead of entire thing, use the **--oneline** flag as follows:
`git log --oneline`

To see which files were altered, we can use the --stat flag along with git log
Syntax: `git log --stat`

To see the exact patches made in any file change, we can use the -p flag:
Syntax: `git log -p`

To ignore all the whitespace changes , we can use the -w flag:
Syntax: `git log --stat -p -w`

There are lots of other flags which can be used, see the documentation [here](https://git-scm.com/docs/git-diff)

## show

Shows all the information about a single commit, depending on the SHA
Syntax: `git show <SHA first 7 chars>`

Note that we can use all the flags used in `log` in this command as well.

## add

We add untracked files to the staging area using this command. This command takes a space-separated list of file names alternatively, the period . can be used in place of a list of files to tell Git to add the current directory (and all nested files)

Syntax: `git add <file1> <file2> … <fileN>`

## commit

Move the added files from the staging area to the local repo using commit command. The message that is needed along with this can be typed using the code editor or by using the **-m** flag.

If the commit msg is tyoed in the code editor, type it in the first line of the editor.
Syntax: `git commit -m "Initial commit"`

The goal is that each commit has a single focus. Each commit should record a single-unit change. Hence choose a suitable commit message.

Do's and Dont's of a commit message:

### Do

-   do keep the message short (less than 60-ish characters)
-   do explain what the commit does (not how or why!)

### Do not

-   do not explain why the changes are made (more on this below)
-   do not explain how the changes are made (that's what git log -p is for!)
-   do not use the word "and". If you have to use "and", your commit message is probably doing too many changes - break the changes into separate commits
    e.g. "make the background color pink and increase the size of the sidebar"
    The best way that I've found to come up with a commit message is to finish this phrase, "This commit will...". However, you finish that phrase, use that as your commit message.
-   Above all, be consistent in how you write your commit messages!

_That is, If you need to explain why a commit needs to be made, you can!_

_When you're writing the commit message, the first line is the message itself. After the message, leave a blank line, and then type out the body or explanation including details about why the commit is needed (e.g. URL links)._

[Here](https://udacity.github.io/git-styleguide/) is a style guide to help type useful commit messages.

## diff

This command can be used to see changes that have been made but haven't been committed, yet.
`git log -p` uses `git diff` under the hood.

## .gitignore

This file will have all the files that we do not want to add to the staging area. We can specify the entire filename, or just the file extensions using the wildcard character (For eg, \*.docx)

### Globbing

In order to use .gitignore to ignore many files of same type, we need not type each file's name in .gitignore, instead we can use the concept of globbing.
Globbing lets you use special characters to match patterns/characters. In the .gitignore file, you can use the following:

1. blank lines can be used for spacing
2. \# - marks line as a comment
3. \- \- matches 0 or more characters
4. ? - matches 1 character
5. [abc] - matches a, b, _or_ c
6. \* - matches nested directories - a/\*\*/z matches
   i. a/z
   ii. a/b/z
   iii. a/b/c/z

## tags

The tags help certain commits stand out amongst the other ones, such as version 1.0
Syntax: `git tag -a v1.0`

Note the **-a** flag used in the above command, which helps in creating an annotated flag. Excluding this will create a _lightweight_ tag.

Annotated tags are recommended because they include a lot of extra information such as:

-   the person who made the tag
-   the date the tag was made
-   a message for the tag
-   Because of this, you should always use annotated tags.

**Note:** If you just type `git tag` it returns a list of all tags in the commit history.
The `git log` command displays the tag in the SHA line itself, no need to use any other flags.

In order to delete a tag that was created by accident, then use the following command:
`git tag -d <tag name>`

By default, the tag gets added to the most recent commit, but we can also specify the commit we want to tag, by specifying the commit SHA along with the tag command, as follows:

`git tag -a <tag name> <SHA>`

Note: The tags are like permanent pointers and are specific to the commits, they do not move fwd or backwards based on new commits

## Branches

Git allows us to have as many number of branches as needed, and the default one is **main** or **master**. If we now create a new branch called **sidebar**, and intend to use this branch as our current repo, we will need to use the `checkout` command.

To check all the available branches, we will need to use the `git branch` command.

It can also be used to:

-   list all branch names in the repository
-   create new branches
-   delete branches

In order to create a new branch, the syntax is `git branch <name>`.

Note that this will not automatically change the HEAD to the new branch.

### Checkout

To change from 1 branch to another we have to use this command.
**Syntax:** `git checkout <name>`

It's important to understand how this command works. Running this command will:

-   remove all files and directories from the Working Directory that Git is tracking (files that Git tracks are stored in the repository, so nothing is lost) go into the repository and pull out all of the files and directories of the commit that the branch points to (So this will remove all of the files that are referenced by commits in the master branch.)
-   It will replace them with the files that are referenced by the commits in the sidebar branch.

The active branch will be displayed with an \* next to it, and **HEAD** will point to the active branch.

To delete any branch, use the **-d** flag along with the `branch` command, as follows:

**Syntax**: `git branch -d <name>`

**Note** In order to create a new branch and switch to it automatically, we can use the **-b** flag along with the `checkout` command, as follows:

**Syntax**: `git checkout -b <name>`

## Merge

Combining branches together is called merging. Git can automatically merge the changes on different branches together.

**Syntax:** `git merge <name-of-branch-to-merge-in>`

When a merge happens, Git will:

-   look at the branches that it's going to merge
-   look back along the branch's history to find a single commit that both branches have in their commit history
-   combine the lines of code that were changed on the separate branches together
-   makes a commit to record the merge

Note that the `<name-of-branch-to-merge-in>` indicates what branch to merge with the active branch.

Usually, there are 2 types of merges, a **fast-forward** merge, and a **recursive** strategy merge.

### What if a merge fails?

The merges we just did were able to merge successfully. Git is able to intelligently combine lots of work on different branches. However, there are times when it can't combine branches together. When a merge is performed and fails, that is called a _merge conflict_.

Read [this](https://git-scm.com/book/en/v2/Git-Branching-Basic-Branching-and-Merging#Basic-Merging) and [this](https://git-scm.com/docs/git-merge) for more info.

### Merge conflicts

Most of the time Git will be able to merge branches together without any problem. However, there are instances when a merge cannot be fully performed automatically. When a merge fails, it's called a merge conflict.

If a merge conflict does occur, Git will try to combine as much as it can, but then it will leave special markers (e.g. >>> and <<<) that tell you where you (yep, you the programmer!) needs to manually fix.

**Resolving A Merge Conflict**:

Git is using the merge conflict indicators to show you what lines caused the merge conflict on the two different branches as well as what the original line used to have. So to resolve a merge conflict, you need to:

1. choose which line(s) to keep
2. remove all lines with indicators

Once you've removed all lines with merge conflict indicators and have selected what heading you want to use, just save the file, add it to the staging index, and commit it!

Just like with a regular merge, this will pop open your code editor for you to supply a commit message. Just like before, it's common to use the provided merge commit message, so after the editor opens, just close it to use the provided commit message.

#### To resolve the conflict in a file:

1. locate and remove all lines with merge conflict indicators
2. determine what to keep
3. save the file(s)
4. stage the file(s)
5. make a commit

Be careful that a file might have merge conflicts in multiple parts of the file, so make sure you check the entire file for merge conflict indicators - a quick search for `<<<` should help you locate all of them.

More documentation [here](https://git-scm.com/book/en/v2/Git-Branching-Basic-Branching-and-Merging#Basic-Merge-Conflicts)

### Undoing Changes

We can amend **the most recent** commits we have made, using the **--amend** flag along with the commit command.

**Syntax**: `git commit --amend`

This allows us to change the most recent commit message/add any minor changes to the prev commit, rather than a new commit being made.

In order to add any new changes to the previous commit (related to the prev commit, obviously), then:

1. edit the file(s)
2. save the file(s)
3. stage the file(s)
4. run `git commit --amend`

### Revert a commit

When you tell Git to revert a specific commit, Git takes the changes that were made in commit and does the exact opposite of them. Let's break that down a bit. If a character is added in commit A, if Git reverts commit A, then Git will make a new commit where that character is deleted. It also works the other way where if a character/line is removed, then reverting that commit will add that content back!

**Syntax**: `git revert <SHA-of-commit-to-revert>`

This command:

1. will undo the changes that were made by the provided commit
2. creates a new commit to record the change

[Here](https://git-scm.com/docs/git-revert) is the official docs.

### Resetting a commit

At first glance, resetting might seem coincidentally close to reverting, but they are actually quite different. Reverting creates a new commit that reverts or undos a previous commit. Resetting, on the other hand, erases commits!

Git does keep track of everything for about 30 days before it completely erases anything. To access this content, you'll need to use the git reflog command. Check out these links for more info:

-   [git reflog](https://git-scm.com/docs/git-reflog)
-   [rewrite history](https://www.atlassian.com/git/tutorials/rewriting-history)

#### Relative Commit References

There are special characters called **Ancestry References** that we can use to tell Git about these relative references. Those characters are:

-   ^ –> indicates the parent commit
-   ~ –> indicates the first parent commit

Here's how we can refer to previous commits:

-   the parent commit – the following indicate the parent commit of the current commit

    -   HEAD^
    -   HEAD~
    -   HEAD~1

-   the grandparent commit – the following indicate the grandparent commit of the current commit

    -   HEAD^^
    -   HEAD~2

-   the great-grandparent commit – the following indicate the great-grandparent commit of the current commit
    -   HEAD^^^
    -   HEAD~3

The git reset command is used to reset (erase) commits
**Syntax:** `git reset <reference-to-commit>`

It can be used to:

-   move the HEAD and current branch pointer to the referenced commit
-   erase commits
-   move committed changes to the staging index
-   unstage committed changes

There are 3 flags that can be used along with the reset command: **--mixed**, **--soft**, **--hard**

**--mixed** is the default flag used with the reset command, which sends the files content back to the **working directory.**

**--soft** will take the changes made in commit `<SHA>` and move them directly **to the Staging Index**.

**--hard** will take the changes made in commit `<SHA>` and erases them.

**Note:** It is usually a good idea to backup the current active branch using the backup command, before resetting the branch. Syntax: `git branch backup`

If you created the backup branch prior to resetting anything, then you can easily get back to having the master branch point to the same commit as the backup branch.

You'll just need to:

-   remove the uncommitted changes from the working directory
-   merge backup into master (which will cause a Fast-forward merge and move master up to the same point as backup)
