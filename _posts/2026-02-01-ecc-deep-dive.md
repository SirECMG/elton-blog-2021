---
layout: post
title:  "Deep Dive into Elliptic Curve Cryptography (ECC)"
author: "Elton Murillo"
date:   2026-02-01 12:00:00 +0800
categories: cryptography, math, blockchain
---

Elliptic Curve Cryptography (ECC) is the backbone of modern digital security. From securing your WhatsApp messages to protecting the entire Bitcoin network, ECC provides the mathematical "trapdoor" that allows us to share secrets and sign transactions securely.

In this post, we’ll move beyond the surface-level "what" and dive into the "how"—explaining the math of point arithmetic, the security of the Discrete Log Problem, and how these concepts are used in real-world protocols.

## 1. The Foundation: The Equation
At the heart of ECC is the elliptic curve equation, typically represented in the **Weierstrass form**:

$$y^2 = x^3 + ax + b$$

For a curve to be useful for cryptography, it must be non-singular (it can't have sharp points or self-intersections). This is guaranteed if $4a^3 + 27b^2 \neq 0$.

While we can visualize these curves using real numbers (where they look like smooth curves), cryptography uses **Finite Fields** ($\mathbb{F}_p$). By calculating the equation modulo a large prime $p$, we move from a continuous curve to a set of discrete points. Visually, this looks like a "scatter plot," but mathematically, it preserves the same properties we need for security.

## 2. The Mechanics: Point Arithmetic
The magic of ECC lies in the fact that these points form an **Abelian Group**. This means we can "add" two points on the curve to get a third point on the curve.

### Point Addition (The Chord Method)
To add two distinct points $P_1$ and $P_2$:
1.  Draw a straight line through $P_1$ and $P_2$.
2.  The line will intersect the curve at a third point, $R$.
3.  Reflect $R$ across the x-axis to get $P_1 + P_2$.

Algebraically, for $P_1 = (x_1, y_1)$ and $P_2 = (x_2, y_2)$:
*   $s = \frac{y_2 - y_1}{x_2 - x_1}$
*   $x_3 = s^2 - x_1 - x_2$
*   $y_3 = s(x_1 - x_3) - y_1$

### Point Doubling (The Tangent Method)
When we want to add a point to itself ($P + P$), we cannot draw a line through two points. Instead, we use the **tangent line** at $P$:
*   $s = \frac{3x_1^2 + a}{2y_1}$
*   $x_3 = s^2 - 2x_1$
*   $y_3 = s(x_1 - x_3) - y_1$

### The Identity Element
Every group needs a "zero." In elliptic curves, this is the **Point at Infinity** ($\mathcal{O}$). Adding $\mathcal{O}$ to any point $P$ simply results in $P$.

## 3. The Trapdoor: Scalar Multiplication & ECDLP
The "trapdoor" function that makes ECC secure is **Scalar Multiplication**. This is the process of adding a point $G$ to itself $k$ times:

$$Q = k \cdot G$$

Because point addition is associative, we can use the "Double-and-Add" algorithm (similar to binary exponentiation) to calculate $Q$ very quickly, even if $k$ is a massive number.

However, the inverse operation—finding $k$ when given $Q$ and $G$—is the **Elliptic Curve Discrete Log Problem (ECDLP)**. There is no known efficient way to "undo" scalar multiplication in a large finite field. This is our security guarantee.

## 4. Practical Applications
How do we turn these math points into actual security?

### Key Exchange (ECDH)
Two parties, Alice and Bob, can agree on a shared secret over an insecure channel:
1.  Alice has private key $e_A$ and public key $P_A = e_A \cdot G$.
2.  Bob has private key $e_B$ and public key $P_B = e_B \cdot G$.
3.  They exchange public keys.
4.  Alice computes $S = e_A \cdot P_B$.
5.  Bob computes $S = e_B \cdot P_A$.
Both arrive at the same secret point $S = (e_A \cdot e_B) \cdot G$.

### Digital Signatures (ECDSA & EdDSA)
To sign a message $z$:
1.  Pick a random $k$ and compute $R = k \cdot G$. Let $r$ be the x-coordinate.
2.  Calculate $s = \frac{z + r \cdot e}{k} \pmod n$.
3.  The signature is $(r, s)$.

To verify:
1.  Compute $u = z/s$ and $v = r/s$.
2.  Compute $R' = u \cdot G + v \cdot P$.
3.  If the x-coordinate of $R'$ matches $r$, the signature is valid.

### Encryption (ECIES)
In practice, we rarely encrypt large amounts of data with ECC directly. Instead, we use ECC to perform a key exchange (like ECDH) to derive a symmetric key (like AES), which is then used to encrypt the actual data.

## Conclusion
ECC provides a powerful way to achieve high security with smaller keys than RSA. By combining the geometry of elliptic curves with the modular arithmetic of finite fields, we create a system where multiplication is easy, but division is impossible.

---
*Check out the [secp256k1](https://github.com/jimmysong/programmingbitcoin/blob/master/ch03.asciidoc) parameters for the curve used in Bitcoin!*
