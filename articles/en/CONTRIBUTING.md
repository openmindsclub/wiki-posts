# Git commit messages 

Learn how to make good commits with me since I **HATE** bad commits, as it can ruin the history of an entire project.

## 1. First of all : 
- Stop using -m (as in `git commit -m "commit message"`). Instead just do `git commit` to be able to add a description to your commit messages.
- Change your git default editor if you're not comfortable with vim, nano or emacs (you should use vim its great :3)

You can change it by doing so :
	```
	git config --global core.editor "editor name"
	```

For vsCode users simply do 
	```
	git config --global core.editor "code --wait"
	```

As this [article  says](https://dev.to/biancapower/how-to-change-your-default-text-editor-for-git-and-avoid-vim-fk0). What it will do is open up a vsCode window when you want to write your commit mesage's Title and Body.

## 2. Structure of the commit

- When you do `git commit` as advised above (and after correctly modifying your git default editor), you'll be prompted with something like this:

```
# Please enter the commit message for your changes. Lines starting
# with '#' will be ignored, and an empty message aborts the commit.
#
# On branch master
#
# Initial commit
#
# Changes to be committed:
#       new file:   kern.asm
#       new file:   kert.c
#       new file:   link.ld
#
```

Here you can see the files that will be commited and other infos.

**What you'll do is** 
- On the top, write the title (we will discuss the format later)
- And for the body, you'll keep one blank line and then write the description (if you need to, sometimes you don't)

Here's an example of what it would look like:

```
[feat] add version one of the mini kernel

This is the commit description, you can put here additional info you want other contributors to know about the modifications
# Please enter the commit message for your changes. Lines starting
# with '#' will be ignored, and an empty message aborts the commit.
#
# On branch master
#
# Initial commit
#
# Changes to be committed:
#       new file:   kern.asm
#       new file:   kert.c
#       new file:   link.ld
#
```

## 3. HOW TO WRITE A GOOD COMMIT

- Read this https://betterprogramming.pub/write-better-git-commit-messages-to-increase-your-productivity-89fa773e8375 
- As a "first" good practice we can stick with this syntax:

```
[feat]: introduce a new feature
[fix]: patches a bug in your codebase (bugfix or hotfix)
[build]: changes that affect the build system or external dependencies
[chore]: updates dependencies and does not relate to fix or feat and does not modify src or test files
[ci]: changes that affect the continuous integration process
[docs]: updates the documentation or introduce documentation
[style]: updates the formatting of code; remove white spaces, add missing spaces, remove unnecessary newlines
[refactor]: reactors code segments to optimize readability without changing behavior
[perf]: improve performance
[test]: add/remove/update tests
[revert]: reverts one or many previous commits
```

- A typical commit will look like this:

	```
	[feat] add negamax.
	```
- And with a commit description:

	```
	[fix] negamax infinite looping issue
	
	* the problem was blablabla
	```



