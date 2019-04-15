# To install, run this command
``` bash
bash -c "$(curl https://raw.githubusercontent.com/bokwoon95/setup/master/gitconfig.sh)"
```

**This will not overwrite your existing settings/aliases in your `~/.gitconfig` file, it only adds to it.**

# Why this exists
I wanted a command that I could run on any machine and immediately have my git aliases configured.

Some benefits are:

1) Simple to understand  
These aliases were designed for people who might never use git otherwise.
It is simple enough for them to understand how to use a subset of git for version control immediately.

2) Never gets outdated  
All it does is configure a bunch of git aliases. If you want to know how an alias is doing something, just look inside your `~/.gitconfig` file.
Because it's just chaining native git commands with shell functions, even if I stop maintaining this repository these aliases will continue to work.

It also contains all my convenience aliases, but you don't need to know those when starting out. However, do note that you can type `g` instead of `git` for all commands (e.g. `g l` to show the git log).


# Cheatsheet
```
s                     git status
l                     Shows the commit log

commits [msg]         Make new commit with a message
commitpush [msg]      Make new commit with a message & push to GitHub
pulll                 git pull without overwriting local files

goto [commit]         Goto a particular commit
fixpush               Fixes a failed push if you forgot to pull before pushing
forcepull             Forcibly overwrite your repo with GitHubs repo
forcepush             Forcibly overwrite Githubs repo with your repo
undocommit            Undo your last commit from the git log
                      The changes will still be there, just uncommitted
```
`git cheatsheet` will show this cheatsheet

# Basic Commands
`git s` display what files have been changed, etc

`git l` display the commit history. Uses reflog so that branches beyond master are visible.

`git commits [message]` Saves a commit with a message

`git push` Pushes your unpushed commits to GitHub

`git commitpush [message]` Combination of commits and push

`git pull` Pulls the latest commits from GitHub. Rebase is set as the default instead of merge because it's more intuitive for beginners.

`git pulll` Pulll will allow you to pull the lastest commits when you still have uncommitted changes.

# When things go wrong

`git fixpush` When someone else has already pushed and you try to push as well, GitHub will reject your push. fixpush will pull the latest changes in first, thus allowing you to push. If the latest changes conflict with the changes you are about to push, you have to fix the merge conflict before pushing.

`git goto [commit]` Once something goes wrong you can rollback to a previous commit, using the commit's hash found by git history. (Note that goto is not equivalent to checkout, because goto doesn't go into detached head mode. It will automatically move master along with the head)

`git forcepush` Forcibly make the repo on GitHub the same as yours

`git forcepull` Forcibly make your repo the same as the one on GitHub

`git show [commit]` Display the code changes for a particular commit

`git undocommit` Undo the latest commit. Very useful when you have pushed a commit and realize you need to make one small change. Just undocommit, make your changes, commit again and forcepush.

# Not implemented yet

`git stache` Stash whatever's in the current directory.

`git unstache` Unstash the last stash you saved.

`git dropstache` Drop all stashes

`git reveal [alias]` pretty print out the alias definition

`git dropchanges [file(s)]` Resets the file(s) to the master version. If no arguments are given, reset the entire directory.

`git difference [commit(s)]` make sure difftool=vim and algorithm=patience, plus q for quitting :qa!). If no commits are provided, 'head' will be compared with the unsaved changes. If one commit is provided, that commit will be compared with 'head'. If both commits are provided, they are compared with each other.

`git backup` Copies your modified files out to the desktop. You can then delete the local repo and clone in a fresh copy from GitHub. This is the most [foolproof way of fixing git issues](https://xkcd.com/1597/) when all else fails.

`git cheatsheet-full` Show every single alias provided, including the convenience aliases as well as some alias functions like `checkdangling` or `prunedangling`. Provides a more detailed explanation of what each alias does.

# Example workflows

**Demo 1:** Commit, commit, commit, goto some commit in the past. All history is preserved (as a tree), so you can always find the right commit to goto.  
`git commits`, `git goto`

**Demo 2:** You make some changes, commit and push. Later your friend makes another change and pushes, so you pull in his changes before making any more changes.  
`git commitpush`, `git pull`, `git commitpush`

**Demo 4:** Writing, commitpush, push rejected. Simply fixpush, fix any merge conflicts, then commitpush again. Or, always remember to do a pull before commitpushing.  
`git commitpush`, `git fixpush`, `git commitpush`

**Demo 4:** Writing, commitpush, oh no I need to make one small change! Simply undocommit, make changes, then commits and forcepush. Because you're modifying GitHub commit history, not just adding to it, you need to forcepush.  
`git undocommit`, `git commits`, `git forcepush`
