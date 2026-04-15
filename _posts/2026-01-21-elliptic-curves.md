---
layout: post
title:  "Elliptic Curves"
author: "Elton Murillo"
date:   2026-01-21 11:22:00 +0800
categories: git
---

An elliptic curve is an equation of:


> y^2 = x^3 + bx + c

What makes elliptic curve interesting is that they define a math structure with properties that make them useful for key exchange, and digital signature in the context of cryptography.

Graphically when plotted with real numbers, they represent a curve. But when graphed using finite fields visually it looks like a scatter plot.

Elliptic curves are useful because of "point addition". Point addition is where we can do an operation on two of the points on the curve and get a third point also on the curve. With point addition points behave more like numbers, you can combine them, repeat the operation and build harder operations from simipler ones.

This enables an important property.

    - it is easy to compute nP if you know n.
    - it is hard to go backwards and find n from P and nP


If you look closely, this property is a great set-up for public-key generation from a private scalar, key exchange and digital signatures.

## Math Foundations of EC

### math properties of point addition

- identitiy
- commutativity
- associativity
- invertibility

### deriving the point addition formula

### point addition for when x1 != x2

### point addition for when x1 == x2

### point addition for P1 == P2

### point addition for tangent (exception)


## Elliptic Curve Cryptography

## EC over Reals

## EC over Finite Fields

## Point Addition over Finite Fields

## Scalar Multiplication for Elliptic Curves

## Discrete Log Problem

## Mathematical Groups

### Identity

### Closure

### Invertibility

### Commutativity

### Associativity


## Defining Curve for Bitcoin


### How Big is 2^256

## Public Key Cryptography

### Signing

#### Inscribing the target

#### Signing in Depth

#### Creating a signature

### Verifying

#### Verification in Depth

### Importance of a Unique k
