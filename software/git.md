# Git

## Overview

* @Author: TimsManter
* @AuthorSite: [TimsManter.NET](http://timsmanter.net/)  
* @CreationDate: 2017-01
* @BasedOn: [Codecademy][basedon]

[basedon]: http://codecademy.com/

<!-- TOC -->

- [Overview](#overview)
- [Config](#config)
- [Common](#common)
- [Backtrack](#backtrack)
- [Branches](#branches)
- [Teamwork](#teamwork)
- [Bare repository](#bare-repository)
- [Interactive Rebase](#interactive-rebase)
  - [Change author info on example](#change-author-info-on-example)

<!-- /TOC -->

## Config

`git config --global user.name "Name"`
`git config --global user.email email@example.com`

## Common

Syntax | Description
-------|------------
`git add <file1>[ <file2> <file3> ...]` | add files to staging area.
`git status` | check modications of files.
`git commit -m "Message"` | commit files with message.
`gir commit --amend` | rewrite last commit message.
`git diff` | show differences.
`git log` | list commits.

## Backtrack

Syntax | Description
-------|------------
`git checkout HEAD <filename>` | discard changes in working directory.
`git reset HEAD <filename>` | unstage changes int staging area.
`git reset <sha>` | revert to commit with particular sha.

## Branches

> Note: The one with * on the beggining is the current one.

Syntax | Description
-------|------------
`git branch` | list branches.
`git branch <new_one>` | create branch.
`git branch -d <branch_name>` | delete branch.
`git branch -m <old_name> <new_name>` | rename branch.
`git branch -m <new_name>` | rename current branch.
`git checkout <branch_name>` | change current branch.
`git merge <some_branch>` | merge some_branch with current one.

## Teamwork

Syntax | Description
-------|------------
`git clone remote_repo_name[ my_repo_name]` | clone remote repository.
`git remote -v` | show remote address.
`git fetch` | download changes from remote repo to local origin/repo.
`git push origin <branch_name>` | upload changes from branch_name to origin.
`git remote add upstream <remote_repo_address>` | add upstream address.
`git fetch upstream` | download changes of original upstream repo.

## Bare repository

> NOTE: Useful for dot files.

Syntax | Description
-------|------------
`git --bare init` | init bare repository.
`git --git-dir="$HOME/.cfg" --work-tree="$HOME" <command>` | using bare repository.

## Interactive Rebase
### Change author info on example

- Commits: A - B - C - D - E
- Rebase: From B to D

1. `git rebase -i --root`
2. Change commits B, C, D mode to `edit` or just `e`
3. `git commit --amend --author="Name <email@example.com>" --no-edit`
4. `git rebase --continue`
5. Repeat steps 3. and 4. for the rest of the commits
6. Done