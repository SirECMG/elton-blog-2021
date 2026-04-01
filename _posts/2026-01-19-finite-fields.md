---
layout: post
title:  "Finite Fields"
author: "Elton Murillo"
date:   2026-01-19 10:14:00 +0800
tags: [bitcoin, cryptography]

# TLDR
Finite fields, also known as Galois fields, are number systems with a finite number of elements.

They support addition, subtraction, multiplication, and division, except that division by zero is not allowed. A key property of a finite field is closure: when you perform these operations on elements in the field, the result stays within the same field.

Finite fields usually have a size equal to a prime number or a power of a prime. One simple example is arithmetic modulo 7, where the only possible values are 0 through 6.

Finite fields are important in cryptography because they provide a precise and predictable mathematical system that computers can handle efficiently. Their structure makes them especially useful for algorithms that need exact arithmetic rather than approximations.

They form the mathematical foundation for elliptic curve cryptography, which is widely used in modern systems for public-key cryptography, digital signatures, and secure communication.

## Code Example

```ruby
class FiniteElement
    def initialize(num, order)
        @num = num
        @order = order
    end
end
```

