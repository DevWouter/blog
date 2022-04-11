---
title: "Git Tricks"
date: 2022-04-11T20:57:47+02:00
draft: false
---

A few of my favorite tricks with GIT.

<!--more-->

## Creating a new branch and switching to it

```sh
git checkout -b <branch-name>
```

## Git pushup

This is an alias you put in your `.gitconfig`

```
[alias]
  pushup = !git push --set-upstream origin `git symbolic-ref --short HEAD`
```

Now you can push a branch to remote using `git pushup`.

## Finding a commit

In this one I'm looking for all Merged PRs.

### Powershell

```ps
git log --all --oneline | Select-String -Pattern 'Merged PR \d+'
```

### Linux

```bash
git log --all --oneline | egrep 'Merged PR [[:digit:]]+'
```

## Which branches have a commit

```sh
git branch --contains <git-commit>
```

## Remove branches merged in main

Add the following to your powershell profile

```
function Remove-MergedBranches
{
  git branch --merged |
    ForEach-Object { $_.Trim() } |
    Where-Object {$_ -NotMatch "^\*"} |
    Where-Object {-not ( $_ -Like "*master" )} |
    Where-Object {-not ( $_ -Like "*main" )} |
    ForEach-Object { git branch -d $_ }
}
```

Now after (you perform `git pull`) you can remove all old branches that are merged in another branch.

```ps
Remove-MergedBranches
```