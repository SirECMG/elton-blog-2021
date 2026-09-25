---
layout: post
title:  "Debug bitcoin core using GDB"
date:   2026-09-25 00:01:25 -0700
tags: [ bitcoin ]
---

# compile bitcoind with debug flags

```text
cmake -B build -DCMAKE_BUILD_TYPE=Debug
cmake --build build -j32
```

# run gdb against the binary file

```text
gdb --tui --args ./bitcoind -regtest
```

# make your breakpoint
```text
b src/wallet/wallet.cpp:CreateWallet
```

# in a different terminal invoke bitcoind with bitcoin-cli
```text
./bitcoin-cli -regtest createwallet "elton_wallet0"
```

# if bitcoind is already running 
```text
// inside gdb
attach [process_id]
```


# when running gdb

- it will start showing logs, you can get out of this by control+c, this will bring you back to gdb
- you can press c to go back to logs
