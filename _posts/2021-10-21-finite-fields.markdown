---
layout: post
title:  "Finite Fields"
date:   2021-10-21 21:49:30 -0700
categories: bitcoin-programming
---


# chapter 1: finite field notes

- elliptic curve cryptography
  - signing
  - verification
  - in heart of tranactions
  - transactions atomic unit of value transfer
  - **finite fields**
  - **elliptic curves**


## Finite Field Definition

> finite field is defined as a finite set of numbers and two operations + (addition) and * (multiplication) that satisfy the following:

1. if a and b are in the set, a + b and a * b are in the set. **We call this property closed**.
2. 0 exists and has the property a + 0 = a. **We call this the additive identity**.
3. 1 exists and has the property a * 1 = a. **We call this the multiplicative identity**.
4. If a is in the set, -a is in the set, which is defined as the value that makes a + (-a) = 0. **This is what we call the additive inverse**
5. If a is in the set and is not 0, a^-1 is in the set, which is the value that makes a * a^-1 = 1. **This is what we call the multiplicative inverse**. 


At high level
> we have a set of numbers that's finite. Because the set is finite, we can designate a number p, which is how big the set is. **That is what we call the order of the set**

> #1 We can define addition and subtraction differently than the one you are familar with

> #2 we have addition and multiplicative identities

> #4 we have additive inverse

> #5 we have multiplicative inverse


## Defining Finite Sets

> If the order(or size) of the set is p, we can call the elements of the set, 0,1,2,..,p-1

> These numbers are what we call the elements of the set, not necessarily the traditional numbers 0,1,2,3, etc. They behave in many ways like traditional numbers, but have some differences in how we add, substract, multiply, and so forth.

Math notation
> F_p = {0,1,2, ..., p - 1}

A finite field of order 11:
> F_11 = {0,1,2,3,4,5,6,7,8,9,10}

A finite field of order 17:
> F_17 = {0,1,2,3,4,5,6,7,8,9,10,11,12,13,14,15,16}

> Notice the order of the field is always 1 more than the largest element. You might have noticed that the field has a prime order every time. For a variety of reasons that will become clear later, it turns out that the fields must have an order that is a power of a prime, and **that the finite fields whose order is prime are the ones we're interested in**.

## Modulo Arithmetic

> One of the tools we can use to make finite field closed under addition, subtraction, multiplication, and vision is module arithmetic.

> whenever the division wasn't even there was something called the "remainder" which is the amount left over from the actual division. We define module in the same way. We use the operator % for modulo:

> modulo operation is teh remainder after division of one number by another.

Example(s):

> 7 % 3 = 1
> 1747 % 241 = 60

> You can think of modulo arithmetic as "wraparound" or "clock" math.

It is currently 3 o'clock. What hour will it be 47 hours from now?

> (3 + 47) % 12 = 2pm

It is currently 3 o'clock. What hour was it 16 hours ago?
> (3 - 16) % 12 = 11


The result of the modulo (%) operation is for minutes is always between 0 and 59, inclusive. This happens to be a very useful property as even large numbers can be brought down to a relatively small range with modulo.

We'll be using modulo as we define field arithmetic. Most operations in finite fields use the modulo operator in some capacity.

## Addition and Subtraction

Remember that we need to define finite field addition such that we ensure the result is still in the set (we want to make sure that addition in a finite field is closed.)

we can use modulo arithmetic, to make addition closed

Example

> F_19 = {0,1,2,..18}
> where a,b is in element of F_19.

Addition being closed means:
> a + F_b is in element of F_19

If we utilize modulo arithemtic, we can guarantee this to be the case. We can define a + f_b = (a+b) % p = (a+b) % 19.

We take any two numbers in the set, add, and "wrap around" the end to get the sum. We are creating our own addition operator here and the result is a bit unintuitive. After all, 11 + f_17 = 9 just doesn't look right because we're not used to the finite field addition.

> a + f_b = (a+b) % p where a,b is an element of F_b

We also define the additive inverse this way. 
a is element of F_b implies that -f_a is an element of F_b.
> -f_a = (-a) % p 

**finite field substraction is not the same as integer subtraction**

## Multiplication and Exponentiation

Just as we defined a new addition for finite fields that was closed, we can also define a new multiplication for finite fields that's closed. 

By multiplying the same number many times, we can also define exponentiation. In this section, we'll go through exactly how to define this using modulo arithmetic.

In a finite field, we can do exponentiation using modulo arithmetic:

F_19:

> 7^3 = 343 % 19 = 1
> 9^12 = 7

Again, finite fields have to be defined so that the operation always results in a number within the field.

## Division

The intuition that helps us with addition, subtraction, multiplication, and perhaps even exponentiation unforunately doesn't help us quite as much with division. Because division is the hardest operation to make sense of, we'll start with something that should make sense.

In normal math, division is the inverse of multiplicaion:

7 * 8 = 56 implies that 56/8 = 7
12 * 2 = 24 implies that 24/12 = 2

And so on. We can use this as the definition of division to help us. Note normal math, you cannot divide by 0.

F_19 we know that:

3 * 7 = 21 % 19 = 2 implies that 2 / 7 = 3
9 * 5 = 45 % 19 = 7 implies that 7 / 5 = 9

This is very unintuitive as we generaly thin o f2 / 7 or 7/ 5 as fractions, not nice finite field elements. Yet that is one of the remarkable things about finite fields: finite fields are closed under division. That is, dividing any two numbers where the denominator is not 0 will result in another finite field element.

The question you might be asking yourself is, how do I calculate 2 / 7 if I don't know beforehand that 3 * 7 = 2? This is indeed a very good question: to answer it, we'll have to use the result from Exercise 7.

In case you didn't get it, the answer is that n^(p-1) is always 1 for every p that is the prime and every n > 0. This is a beautiful result from number theory called Fermat's little theorem. Essentially, the theorem says:

> n^(p-1) % p = 1

where p is prime.

Since we are operating in prime fields, this will always be true.

because division is the inverse of multiplication, we know:

> a / b = a * (1/b) = a * b^-1

We can reduce the division problem to a multiplication problem as long as we can figure out what b^-1 is. There is where Fetmat's little theorem comes into play. We know:

> b^(p - 1) = 1

because p is prime. Thus:

> b^-1 = b^-1 * 1 = b^-1 * b^(p - 1) = b^(p - 2)

or:

> b^-1 = b^(p-2)

In F_19, this means practically that b^18 = 1, which means that b^-1 = b^17 for all b > 0.

so in other word,s we can calculate the inverse using the exponentiation operator. In F_19:

> 2 / 7 = 2 * 7^(19 - 2) = 2 * 7^17 = 46526102797774414 % 19 = 3
> 7 / 5 = 7 * 5^(19 - 2) = 7 * 5^17 = 5340576171875 % 19 = 9

This is a relatively expensive calculation as exponentiating grows very fast. Division is the most expensive operation for that reason. To lessen the expense, we can use the pow function in Python, whichi does exponentiation. In Python, pow(7,17) does the same thing as  7 ** 17. The pow function, however, has an optional third argument that makes our calculation more efficient. Specifically, pow will modulo by the third argument. Thus, pow(7, 17, 19) will give the same result as  7 ** 17 % 19 but do so faster becaseu the modulo function is done after each round of multiplication.


## Fermat's Little Theorem

There are many proofs of this theorem, but perhaps the simplest is using what we saw in Exercises 5 -- namely, that these sets are equal:

> {1,2,3, ..., p-2, p -1} = {n % p, 2n % p, 3n % p(p-2) n % p, (p-1) n % p}

The resulting numbers might not be in the right order, but the same numbers are in both sets. We can then multiply every element in both sets to get this equality.

> 1 * 2 * 3 * ... * (p - 2) % p = n * 2n * 3n * ... * (p-2)n * (p-1) n % p

The left side is the same as (p-1)! * n^(p-1) % p! is the factorial.
On the right side, we can gather up all the n's and get:

> (p-1)! * n^(p-1) % p
> Thus:

> The (p-1)! % p = (p-1)! * n^(p-1) % p

> The (p-1)! on both sides cancel, giving us:

> 1 = n^(p-1) % p

This proves Fermat's little theorem

## Redefining Exponentiation

One last thing that we need to take care of before we leave this chapter is the __pow__ method, which needs to handle negative exponents. For example, a^-3 needs to be a finite field element, but the current code deos not take care of this case. We want, for example, sometihng like this to work:

```
from ecc import FieldElement

a = FieldElement(7,13)
b = FieldElement(8,13)
print(a ** -3 == b)
True
```

Unfortunately, the way we've defined __pow__ simply doesn't handle negative exponents, because the second parameter of the built-in Python function pow is required to be positive.

Thankfully, we can use some math we already know how to solve this. We know from Fermat's little theorem that:

> a^(p-1) = 1

This fact means that we can multiply by a^(p-1) as many times as we want. So, for a^-1, we can do:

> a^(-3) = a^-3 * a^(p-1) = a^(p-4)

This is a way we can do negative exponents. A naive implementation would do something like this:

```
class FieldElement:

def __pow__(self, exponent):
  n = exponent
  while < 0:
    n += self.prime - 1 // we add unitl we get a positive element
  num = pow(self.num, n, self.prime) // we use Python built-in pow to make this more efficient.
  return self.__class__(num, self.prime)
```

Thankfully, we can do even better. We already know how to force a numer out of being negative, using our familar friend %! As a bonus, we can also reduce very large exponents at the same time given at a^(p-1) = 1. This will make the pow function work as hard:

```
class FieldElement:
  def __pow__(self, exponenet):
    n = exponent % (self.prime - 1)
    num = pow(self.num, n, self.prime)
    return self.__class__(num, self.prime)
```

Make the exponent into something within the 0 to p - 2 range, inclusive.

## Why fields are primes

Why fields have to have a prime power number of elements? No matter what k you choose, as long as it's greater than 0, multiplying the entire set by k will result in the same set as you started with.

Intuitively, the fact that we have a prime order results in every element of a finite field being equivalent. If the order of the set was a composite number, multiplying the set by one of the divisors would result in a smaller set.

## Conclusion

This this chapter we learned about finite fields and how to implement them. We'll be using finite fields for elliptic curve cryptography. We turn next to other mathematical component that we need for elliptic curve cryptography: elliptic curves.