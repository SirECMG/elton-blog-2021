---
layout: post
title:  "Finite Fields"
author: "Elton Murillo"
date:   2026-01-19 10:14:00 +0800
categories: git
---

# TDLR
In the context of Bitcoin, Finite Fields are used in the area of public key derivation in conjunction with ellptic curves for the process of generating a public key given a private key, signing and verifying.

Finite Fields is a set of numbers (similar to integers and real numbers) with defined arithmetic operations
and are used because the math operations ensure closed properties when performed. 

Also, finite fields facilitate the math since each operation reduces to simple integer arithmetic modulo a prime.

# Definition of Finite Field
Finite Fields are a set of numbers with finite size.

|F| = p^n (every finite field has a number of elements equal to a prime power.

A finite field has order p^n and is denoted F_{p^n}

F_p = {0,1,..., p - 1}

- where p is a prime number
- n is a positive integer (extension degree)
    - The extension degree (n) determines how elements of the field are structured.
- The order (total number of elements) in the field


# Formal Field Definition
1. Addition & Multiplication: Commutative, associative, with identity elements (0 and 1)
2. Subtraction & Division: Existence of additive and multiplicative inverses
3. Distributive property: a × (b + c) = (a × b) + (a × c)

Finite Fields can only exist of the size of the finite field is of a prime power (p^n). Where p is a prime number and n is the extension degree of the vector space its prime field. In bitcoin case it is 1 but in other ellptic curves it can be different.
