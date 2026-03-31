---
layout: post
title:  "git study codebase guide"
date:   2026-03-31 09:26:00 -0700
tags: [git]
---

Use the following commands to help you study codebases.


## search code history
```bash
# in descending order
git log -G "some_string" -p

# in ascending order
git log --reverse -G "some_string" -p

# Shows the commit history for one file.
git log --reverse -G "some_string" -p -- path/to/file

# history per file and follows renames (better to use --follow than without)
git log --follow --reverse -G "some_string" -p -- path/to/file

# Finds commits where the exact string count changed. Good for tracing introduction/removal of a symbol.
git log -G"def charge|class PaymentProcessor" -p
```

## search commit history


```bash
# search file in codebase filtered by file name

rg "some string" -g "**amount**"
rg "some string" -g "**amount.cpp"
```


## who made last line change for a given file

```bash
git blame src/consensus/amount.h
```


## show one commit in full

```bash
git show <commit_hash>

git show abc123:app/services/payments.rb
```


## compare commits

```bash
# Helps compare current work, nearby commits, or branches.
git diff
git diff HEAD~1..HEAD
git diff main...feature-branch

# Very good for understanding how one file evolved between two points.
git diff abc123 def456 -- app/services/payments.rb
```

## who contributed the most?
```bash
# Shows who has contributed the most commits.
git shortlog -sn
git shortlog -sne
git shortlog -sne -- src/
```

## track a person commit history
```bash
#  That searches commit author names and emails.
git log --author="Alice"
git log --author="Alice|Bob"

# Search commits by author for one file:
git log --author="Alice" -- path/to/file

# Search commits by author for a directory:
git log --author="Alice" -- src/

# See the actual patches they changed:
git log --author="Alice" -p -- src/

# See just filenames they changed:
git log --author="Alice" --name-only --oneline

```

## quick glance on current events
```bash
# see codebase history in compact graph
git log --oneline --graph --decorate --all

# git an idea of what changed (good to skim)
git log --stat
git log -p
```
