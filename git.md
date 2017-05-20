# Git

## Overview

* @Author: TimsManter
* @AuthorSite: [TimsManter.NET](http://timsmanter.net/)  
* @CreationDate: 2017-01
* @BasedOn: [Codecademy][basedon]

[basedon]: http://codecademy.com/

<!-- TOC -->

- [Overview](#overview)
- [Common](#common)
- [Backtrack](#backtrack)
- [Branches](#branches)
- [Teamwork](#teamwork)

<!-- /TOC -->

## Common

`git add <file1>[ <file2> <file3> ...]` add files to staging area.

`git status` check modications of files.

`git commit -m "Message"` commit files with message.

`gir commit --amend` rewrite last commit message.

`git diff` show differences.

`git log` list commits.

## Backtrack

`git checkout HEAD <filename>` discard changes in working directory.

`git reset HEAD <filename>` unstage changes int staging area.

`git reset <sha>` revert to commit with particular sha.

## Branches

`git branch` list branches.
> Note: The one with * on the beggining is the current one.

`git branch <new_one>` create branch.

`git branch -d <branch_name>` delete branch.

`git checkout <branch_name>` change current branch.

`git merge <some_branch>` merge some_branch with current one.

## Teamwork

`git clone remote_repo_name[ my_repo_name]` clone remote repository.

`git remote -v` show remote address.

`git fetch` download changes from remote repo to local origin/repo.

`git push origin <branch_name>` upload changes from branch_name to origin.

`git remote add upstream <remote_repo_address>` add upstream address.

`git fetch upstream` download changes of original upstream repo.