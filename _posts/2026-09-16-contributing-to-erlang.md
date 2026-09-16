---
layout: post
title:  "configure llama.cpp on fedora"
date:   2026-09-16 03:40:00 -0700
tags: [beam]
---

# Contributing to Erlang

[prereq's](https://github.com/erlang/otp/blob/master/HOWTO/INSTALL.md#required-utilities)
[development docs](https://github.com/erlang/otp/blob/master/HOWTO/DEVELOPMENT.md)

```text
export ERL_TOP=`pwd`
./otp_build configure && make
```

## faster builds

```text
## Change N to be at least the number of cores or hyper-threads available
export MAKEFLAGS=-jN
```

## how to debug

I am still learning how to debug erlang. But what you can do is add io:format on speific test cases.
And when executing individual tests, a website is created for that test result. You will see your log messages there.

I am still exploring other options, I believe you can use erl and debugger:start(). but I need to get familiar with that.
```text
pending..
```


## running specific tests

[testing document](https://github.com/erlang/otp/blob/master/HOWTO/TESTING.md#running-tests-while-developing)

```text
# ERL_TOP needs to be set correctly
cd /path/to/otp
export ERL_TOP=`pwd`


# Build Erlang/OTP
#
# Note that make test will only compile test code except when
# make test is executed from $ERL_TOP.
./otp_build setup -a

# Run a test case
(cd $ERL_TOP/erts/emulator && make test ARGS="-suite binary_SUITE -case deep_bitstr_lists")
make emulator_test ARGS="-suite binary_SUITE -case deep_bitstr_lists"

```
