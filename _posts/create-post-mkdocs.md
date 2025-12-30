---
date:
  created: 2025-06-14
---

# create post
This is my first blog post using mkdocs-material.. 

<!-- more -->

## create a file

create a file under docs/blog/post/[some-file-name].md

```
touch docs/blog/post/new-post.md
```

## give it a metadata

date: is a mandatory header
```
---
  date: yyyy-mm-dd
---
```

[additional metadata to improve experience](https://squidfunk.github.io/mkdocs-material/tutorials/blogs/basic/#edits)


## exclude drafts

```
---
date:
  created: 2024-01-01
draft: true
---
```


## references
- [original guide to create post using mkdocs-material](https://squidfunk.github.io/mkdocs-material/tutorials/blogs/basic/)
