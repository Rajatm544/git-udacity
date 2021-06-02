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
