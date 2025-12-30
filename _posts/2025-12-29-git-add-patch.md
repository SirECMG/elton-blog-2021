---
layout: post
title:  "git add patch"
date:   2025-06-21 05:10:00 -0700
categories: git
---

# git add --patch

This command allows you to concisely add lines of code to a commit.

```
git add --patch
```

## select lines of code
You will then select lines of code that matter to the commit. Each sections of code shown is a **hunk**.

- select 'y' to agree to add hunk
- select 'n' to ignore hunk

## edit hunks
If there is a line of code that does not fit in the hunk. You have to select 'e' to edit the hunk.
Remove lines of code that don't matter by deleting it.

## write your commit message
```
git commit
```


## references

- [git add patch youtube video](https://www.youtube.com/@typecraft_dev/videos)
- [pro git](https://git-scm.com/book/en/v2/Git-Tools-Interactive-Staging)
