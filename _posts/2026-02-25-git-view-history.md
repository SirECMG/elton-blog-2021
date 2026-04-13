---
    layout: post
    title: "view git commit history"
    author: "Elton Murillo"
    date: 2026-02-25 10:33:00 +0800
    tags: git
---

View git commit history in nice graphical format.

oneline
```bash
git log --oneline --graph --all
```
detailed
```bash
git log --graph --all --decorate=short
```

You can use this command to get familiar with recent efforts and understanding merges.

query for time range

```bash
git log --since="2026-01-01"

git log --before="2026-02-01"

git log --since="2026-01-01" --before="2026-02-01"

git log --since="2 weeks ago"
git log --since="3 days ago"
git log --since="yesterday"
```

query for author
```bash
git log --author="Elton"
```

