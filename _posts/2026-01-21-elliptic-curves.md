---
layout: post
title:  "Elliptic Curves in Short"
author: "Elton Murillo"
date:   2026-01-21 11:22:00 +0800
tags: [bitcoin, cryptography]
---

[paper on elliptic curve](https://www.secg.org/sec1-v2.pdf#page=52)

### Overview

An important part of decentralized currency is to enable a feature for sovereignty. Meaning we need features such as digital signatures (signing and verifying ownership of some entity). 

To enable that in code, we use elliptic curves. Elliptic curves allow for provisioning of private and public keys. Using these keys we can sign and verify ownership of data.

This mathematical structure is important as it is used in the heart of important infrastructures like Bitcoin.


### Definition

An elliptic curve is an equation of:

> y^2 = x^3 + ax + b

### Moving Parts of EC

1. G
  - A generator point is a point whose repeated addition produces every point in a particular cyclic subgroup of the elliptic curve. This point is common knowledge to everyone. It is important because it is used in a equation involving pubilc and private keys.

2. p
    - size of the finite field (a prime number)

3. a,b
    - these are arbitrary numbers and act as a parameter to the curve. These along with G are publicly known.

4. n
    - public order of the generator point (not used in main equations)
5. h
    - a cofactor (constant, not used in main equations; in secp256k1 it is set to 1)

## Public Key Equation

>Q = dG

- d (privkey) is a scalar (just a number).
- G is a coordinate.
- Q (pubkey) is a coordinate

This equation describes how public keys are generated given a private key.

Since Q needs to be in the realm of the elliptic curve and Q is a coordinate. If we plugin the values of Q to elliptic curve equation (it should be valid).


### Hypothetical Example

- Q = (10,6) pubkey
- a = 2 known constant
- b = 2 known constant
- p = 17 order of finite field
- G = (5,1) known constant

then plugging in EC equation:

> y^2 = x^3 + ax + b

> 6^2 = 10^3 + 2 * 10 + 2 mod 17 // we mod because EC are based off finite fields

> left side: 36 mod 17 = 2

> right side: 1022 mod 17 = 2

> 2 = 2 // both sides are equal


### Math Properties

Graphically when plotted with real numbers, they represent a curve. But when graphed using finite fields visually it looks like a scatter plot.

Elliptic curves are useful because of “point addition”. Point addition is where we can do an operation on two of the points on the curve and get a third point also on the curve. This is because elliptic curves obey closure properties. More formally, they are classified as a math group. 

With point addition points behave more like numbers we are used to (real numbers) or more accurately math groups. you can combine them, repeat the operation and build harder operations from simpiler ones (since adding points will result on points on the curve).

### discrete log problem
These math properties enables an important property.

- it is easy to compute nP if you know n. (nP means "point P added to itself n times" using elliptic curve point addition.)
- it is hard to go backwards and find n from P and nP


### Use-cases for Elliptic Curve

With these surface level knowledge, we can study the use-case and math more in-depth for elliptic curves. These are key exchange(sharing secrets), digital signatures, verifying signatures, and encryption.

### Down the rabbit hole

Elliptic Curves are a big topic and this post tries to quickly summarize it's importance.
TLDR in the context of bitcoin, they are used for digital signatures, which enables the math and code to support sovereignty in a decentralized environment because everyone running the code uses the same EC configurations (G,a,b).

### Additional links

[technical post on ec](https://davidederosa.com/basic-blockchain-programming/elliptic-curve-keys/)

