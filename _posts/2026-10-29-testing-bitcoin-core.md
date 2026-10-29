---
layout: post
title:  "Testing Bitcoin core"
author: "Elton Murillo"
date:   2026-10-29 11:27:00 +0800
tags: [bitcoin]
---

You have just made a change and want to run all test cases (cpp/python/ci); then run the following commands.

# Testing Bitcoin Core

```text
# 1. Build Bitcoin Core and all enabled test binaries
cmake --build build -j32

# 2. Run all CTest-registered tests (unit tests)
ctest --test-dir build --output-on-failure -j32

# 3. Run extended functional tests for more comprehensive coverage
build/test/functional/test_runner.py --extended --jobs=32

# 4. ci testing
env -i HOME="$HOME" PATH="$PATH" USER="$USER" FILE_ENV="./ci/test/00_setup_env_arm.sh" ./ci/test_run_all.sh
```

