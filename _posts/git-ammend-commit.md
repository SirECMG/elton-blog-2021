---
  date: 2025-08-09
---

# How to ammend a commit
below are quick steps for when you want to modify a previous commit.

```
git add .
```

```
git commit --amend
```

- an editor will pop-up and you can modify the commit message if needed
- as a result, no new commits will be added, instead will modify the previous commit.


```
git push --force
```
- This will overwrite the remote branch, so becareful.
