---
layout: post
title:  "Elliptic Curves"
author: "Elton Murillo"
date:   2026-01-21 11:22:00 +0800
categories: git
---

[paper on elliptic curve](https://www.secg.org/sec1-v2.pdf#page=52)

### Elliptic Curve Overview

### Definition

An elliptic curve is an equation of:

>y^2 = x^3 + ax + b

What makes elliptic curves interesting is that it has math properties that make them useful for key exchange (sharing secrets), digital signatures and encryption in the context of cryptography.

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

[add_reference_wiki_ecc](addlinkhere)
