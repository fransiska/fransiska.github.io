---
layout: post
title: Duck Typing, Inheritance, and Composition
category: programming
tags: [programming]
---

I've been trying to properly learn about Design Pattern. Currently reading a for-dummies-book, `Head First Design Patterns A Brain-Friendly Guide`. I knew about it years ago but never really learn about it. I guess when you just started programming seriously, you can't really grasp the concept. I guess I [grew](https://betterprogramming.pub/top-signs-of-an-over-experienced-programmer-22bbe0b57663#:~:text=Once%20software%20engineers%20hit%20the,what%20company%20you%20work%20for.) a bit. 

In the first chapter of that book, there's a discussion on inheritance and composition.

### Duck Typing

Is when an object is judged by what it can do, not by what it is (the inheritance).

### Inheritance

An `Employee` inherits from class `Person`, ie. to be a subclass of a parent class. The *L* of *SOLID* principle is *Liskov substitution principle*. An instance of `Employee` should be substitutable with an instance of `Person`. So if `Employee` has extra methods, it should not 
