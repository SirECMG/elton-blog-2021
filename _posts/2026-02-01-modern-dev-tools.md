---
layout: post
title:  "modern dev tools starter kit"
date:   2026-02-01 10:42:00 -0700
categories: tools
---

In order to become a better dev in the sense of tackling bigger projects and larger codebases. It is important to leverage tools to become more productive.

During university, we were taught to leverage unix commands to perform useful functions for whatever task we need it.

In todays world, those "legacy" tools are useful and pre-installed on many systems. But, there are other popular tools created by the community that offer better user experiences with more performance and the same functionality.

I will provide a list of what I feel are the essential programs and also notable ones which I feel are probably "nice to haves" outside of the core tools.

## Essentials
- grep -> rg - used to find text in files
- find -> fd - find files
- sed -> sd - replace strings
- cat -> bat - print file contents
- htop -> btm/btop - resource monitor
- ls -> lsd - view directory (might remove this one from list..)
- du -> dust/gdu - disk usage
- vi -> neovim - text editor
- tree - view directory in tree format

## Nice to Haves
- delta (git diff) - git diff viewer

----

# Install commands

## rg

[github](https://github.com/BurntSushi/ripgrep)

ubuntu/debian
```
sudo apt-get install ripgrep
```

windows
```
winget install BurntSushi.ripgrep.MSVC
```




## fd
[github](https://github.com/BurntSushi/ripgrep)

ubuntu/debian
```
sudo apt install fd-find
```

windows
```
winget install sharkdp.fd
```




## sd
[github](https://github.com/BurntSushi/ripgrep)

ubuntu/debian
```
sudo apt install sd
```

windows
```
winget install chmln.sd
```




## bat
[github](https://github.com/sharkdp/bat)

ubuntu/debian
```
sudo apt install bat
```

windows
```
winget install sharkdp.bat
```


## neovim
[github](https://github.com/neovim/neovim)

ubuntu/debian
```
sudo apt install neovim
```

windows
[releases](https://github.com/neovim/neovim/releases/)

## tree

ubuntu/debian
```
sudo apt install tree
```

windows
```
## built into powershell
tree
```
