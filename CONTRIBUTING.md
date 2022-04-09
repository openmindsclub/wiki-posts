# Git commit messages 

Big question  since i **HATE** bad commits (especially hadouk ta3 locklock)

## 1. First if all : 
- stop using that shitty -m (as in `git commit -m "commit message`)
instead just do git commit  but before that 
- Change your git default editor
	- If your not confortable with vim nano or emacs (you should use vim its great :3)
- change your default editor by doing so :
	```
	git config --global core.editor "editor name"
	```
- for vsCode people simply do 
	```
	git config --global core.editor "code --wait"
	```
	As this [article  says](https://dev.to/biancapower/how-to-change-your-default-text-editor-for-git-and-avoid-vim-fk0) 

	What it will do is open up a vsCode windows when you can write your commit mesage's Title and Body (when you do -m you only write the Title)

## 2. Structure of the commit

- When you'll do `git commit`  and you correcly modified your git default edior you'll be prompted with something like this



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
here you can see the files that will be commited the branch in which they will be commited and other infos.
**What you'll do is** 
- on the top write the title (we will discuss the format later) in this message 
- and for the body you'll keep one blanc line and then write it (if you need to, sometimes you don't)
an example will be 
```
[feat] add version one of the mini kernel
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
## HOW TO WRITE A GOOD COMMIT

- just read this https://betterprogramming.pub/write-better-git-commit-messages-to-increase-your-productivity-89fa773e8375 
- so as a "first" good practice we can stick with these , but we can always have a discussion about it if you want


```
[feat]: introduce a new feature
[fix]: patches a bug in your codebase (bugfix or hotfix)
[build]: changes that affect the build system or external dependencies
[chore]: updates dependencies and does not relate to fix or feat and does not modify src or test files
[ci]: changes that affect the continuous integration process
[docs]: updates the documentation or introduce documentation
[style]: updates the formatting of code; remove white spaces, add missing spaces, remove unnecessary              newlines
[refactor]: reactors code segments to optimize readability without changing behavior
[perf]: improve performance
[test]: add/remove/update tests
[revert]: reverts one or many previous commits
```

- a typical commit will be looking like this:

	```
	[feat] add negamax.
	```
- and with additional info 

	```
	[fix] negamax infinite looping issue
	
	* the problem was blablabla
	```


