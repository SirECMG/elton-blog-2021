---
layout: post
title:  "Common bitcoind Scenarios to Debug for Learning"
date:   2026-10-14 00:09:22 -0700
tags: [ bitcoin ]
---

# Overview
Use the following commands to simulate common scenarios to better understand the protocol.
You can create breakpoints in various files and step through the code to understand code flows.


# Setup: start two independent nodes

## Fresh directories for this test.

```text
TEST_ROOT=$(mktemp -d /tmp/bitcoin-rpc-test.XXXXXX)
A_DIR="$TEST_ROOT/a"
B_DIR="$TEST_ROOT/b"
mkdir -p "$A_DIR" "$B_DIR"

bitcoind -regtest -datadir="$A_DIR" -daemon \
  -port=18444 -rpcport=18443 \
  -listen=1 -connect=0 -dnsseed=0

bitcoind -regtest -datadir="$B_DIR" -daemon \
  -port=19444 -rpcport=19443 \
  -listen=1 -connect=0 -dnsseed=0

# Convenience functions. Authentication uses each node's local cookie.
a() { bitcoin-cli -regtest -datadir="$A_DIR" -rpcport=18443 "$@"; }
b() { bitcoin-cli -regtest -datadir="$B_DIR" -rpcport=19443 "$@"; }

a -rpcwait getblockchaininfo
b -rpcwait getblockchaininfo

# Connect A to B using B's P2P port, not its RPC port.
a addnode "127.0.0.1:19444" "add"
a getpeerinfo

```


# Create wallets and fund A

```text
a createwallet "alice"
b createwallet "bob"

aw() { a -rpcwallet=alice "$@"; }
bw() { b -rpcwallet=bob "$@"; }

MINER_ADDR=$(aw getnewaddress "mining")

# Bootstrap funds; coinbase outputs need maturity before spending.
a generatetoaddress 101 "$MINER_ADDR"

aw getbalances

# Wait until B has the same bootstrap chain.
BOOTSTRAP_TIP=$(a getbestblockhash)
until [ "$(b getbestblockhash)" = "$BOOTSTRAP_TIP" ]; do
  sleep 1
done
```




# Create one transaction sending to self

```text
SELF_ADDR=$(aw getnewaddress "self")

TX_SELF=$(aw -named sendtoaddress \
  address="$SELF_ADDR" amount=1 fee_rate=2)

aw gettransaction "$TX_SELF"
a getmempoolentry "$TX_SELF"
```




# Create one transaction sending to another wallet

```text
BOB_ADDR=$(bw getnewaddress "from-alice")

TX_OTHER=$(aw -named sendtoaddress \
  address="$BOB_ADDR" amount=2 fee_rate=2)

a getrawmempool
```




# Create a block containing the mempool transactions

```text
b setnetworkactive false

BLOCK_HASH=$(a generatetoaddress 1 "$MINER_ADDR" | jq -r '.[0]')

a getblock "$BLOCK_HASH" 1 |
  jq '{hash, height, nTx, tx}'`
```


# Transfer the block from A to B and verify chain growth

# Fetch the entire serialized block from A.

```text
BLOCK_HEX=$(a getblock "$BLOCK_HASH" 0)
```

# Submit it through B's RPC interface.
```text
b submitblock "$BLOCK_HEX"
```

# Verify that B activated it.

```text
test "$(b getbestblockhash)" = "$BLOCK_HASH" &&
  echo "B accepted and activated A's block"

b getblockcount
b getblock "$BLOCK_HASH" 1 | jq '{height, confirmations, nTx, tx}'
bw gettransaction "$TX_OTHER" | jq '{amount, confirmations}'
```


# For a real P2P propagation test, reconnect B and mine another block on A:

```text
b setnetworkactive true
```

# Wait for A's persistent addnode connection to reconnect.
```
until [ "$(a getconnectioncount)" -gt 0 ]; do
  sleep 1
done

NEXT_HASH=$(a generatetoaddress 1 "$MINER_ADDR" | jq -r '.[0]')

until [ "$(b getbestblockhash)" = "$NEXT_HASH" ]; do
  sleep 1
done

b getblockcount    # 103
```
