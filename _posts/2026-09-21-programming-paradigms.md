---
layout: post
title:  "Programming Paradigms"
date:   2026-09-21 11:26:00 -0700
tags: [ insights ]
---

# Programming Paradigms

Lately, I have studying various different programming in attempts to get insight on "the fundamentals".

I have dabbled in languages such as:

- elixir
- erlang
- ruby
- rust
- C++/C
- C#/Java

These programming languages gave me some insights on the essence of some of the modern paradigms. And what mainstream programmming languages are trying to incorporate in their feature set. 

In particular, ruby and elixir has given me some insight on these fundamentals. I will publish some short notes on the insights to help me remember what I have learned.

## Object Oriented Programming

Ruby has taught me the following about object oriented programming. In OOP the concept of 
"message passing" is fundamental. In OOP the universe centers around the idea of objects. Objects interact with each other and send messages between them (and possibly itself).
Functions are not an idea in this world (although modern programming languages hide this with sugar syntax). In OOP functions or blocks of code are tucked into methods.

In objects have state and behaviors. It is best practice to send messages. So if you want to broadcast state between objects, it is best to do so through behaviors (aka methods).

The idea behind OOP is to model the real world the way a human would, this makes it easy for us to write code in a way a human would naturally thing, but state can get complicated quickly due to objects loading code from different objects and the developer maintaining and writing the code needs to keep in context all the of the origins of code (the current object uses).

## Functional Programming

Elixir has taught me how functional programming simplifies the programming model by functions. In functional programming, there are just functions and data. Code is localized through functions. Code is organized through Modules. Data is modified in functions by created new states rather than mutating the existing data.

The benefits of this is that programs are easier to maintain, the downsides of this is that performance is not optimal (mutating is more performant than new allocations). But in terms of BEAM VM, garbage collection is fast, due to non-shared state.

## Lower-Level Programming


After analyzing these two programming languages (Ruby and Elixir), Observed and came up with the insight that all other programming languages(mainstream) blend the two and sometimes mix in the idea of incorporating system level programming.

In system level programming languages, the programming languages puts the machine as the center of the universe. You have to keep in context of memory, while you are writing code and what parts of memory owns what and when to free that memory used. C, C++, Rust helps us write code to accomplish this, but you also have to incorporate your business logic.

## Type driven developement

With a language like rust, I have learned the value of types. With types being so strong, we can prove something is correct by leveraging and leaning against the compiler.
For example in Rust, we can write something like the following

```rust

struct Node<T> {
    x: T,
    next: Option<Box<Node<T>>>
};
```

what is interestin is the value of next. The value of next could either be null, or contain an actual value on heap and this can be enforced with the strong type system.
Box is something that is context aware of the heap and combined with options type, the value can either be Some or None. With strong typing the compiler, you get safety through thte type system. 

This makes rust such an interesting programming language. This language actually is more lower-level than a language like C++ which hides or assumes you understand and know what yyou are doing. Rust makes this explict using the type system.

## Conclusion

After spending several months coding in different langauges.

I have personally, took appreciation of

- Erlang
- C/C++/Rust
- JavaScript

And for languages that help pay the bills and give me life there are

- Java/C#
