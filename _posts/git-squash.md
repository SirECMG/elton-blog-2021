---
    date: 2025-07-08
---

# git squash

1. checkout feature branch
```
git checkout bug_fix
```


2. act and operate on previous 3 commits from head
```
git rebase -i HEAD~3
```


3. change the commits you want to collidate to "squash" instead of "pick"
4. "squash" means consolidate to the previous "pick" commit
5. next you will need to edit the commit message of the squashed commit. this will be the updated commit message

## reference video

[video from youtube](https://www.youtube.com/watch?v=V5KrD7CmO4o)