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


how frequently a file changed in repo

```bash
git log --name-only --pretty=format: | sort | uniq -c | sort -nr | head -50
```

search commits for particular strings
```bash
git log -p -G "PaymentProcessor|def charge|class User" -- .
```

search commit messages
```bash
git log --oneline --grep="refactor\|auth\|payment"
```

who commited the most
```bash
git shortlog -sn
```

who changed the most on a particular folder
```bash
git shortlog -sn -- app/services
```

who commited the most in a particular folder
```bash
git shortlog -sn -- app/services
```

shows commit messages in reverse order useful to glance history
```bash
git log --reverse --oneline
```


