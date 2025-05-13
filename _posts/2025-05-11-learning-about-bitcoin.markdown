---
layout: post
title:  "How to Build Bitcoin Core"
date:   2025-05-11 07:19:00 -0700
categories: bitcoin
---

# Getting Started First Steps

## Clone the Repo

bitcoin core (the reference implementation) has great [documentation](https://github.com/bitcoin/bitcoin/blob/master/doc/build-unix.md) to build the project.

```
git clone https://github.com/bitcoin/bitcoin.git
```

## Get the dependencies (Fedora)
```
sudo dnf install gcc-c++ cmake make python3
sudo dnf install libevent-devel boost-devel
sudo dnf install sqlite-devel
sudo dnf install zeromq-devel
sudo dnf install systemtap-sdt-devel
sudo dnf install capnproto
sudo dnf install qt6-qtbase-devel qt6-qttools-devel
sudo dnf install qt6-qtwayland
```
## Build the Project

```
cmake -B build
cmake --build build    # use "-j N" for N parallel jobs
cmake --install build  # optional
```

### [Reference Documentation](https://github.com/bitcoin/bitcoin/blob/master/doc/build-unix.md)

