---
layout: post
title: Functional programming
description: ""
category: programming
tags: [programming, functionalProgramming]
date: 2017-06-02 20:47:19 +07:00
---

As I understand it.

- **Functional programming**: Opposed to object-oriented programming, the return value of a function does not depend on the state of the object, ie. it will always be the same given the same argument.
- **First-class functions**: A language can either have first-class functions or not. It can: return a function, create an array of functions ([source](https://rosettacode.org/wiki/First-class_functions)). 
- **Higher-order functions**: Functions that can take functions as input (arguments) or output (return value).

These three are characteristically used by languages with first class functions. 

- **Anonymous functions**: Functions defined without a name.
- **Closure**: When defining a function inside a function, the inner function has access to the arguments given to the outer function ([source](https://stackoverflow.com/a/36639)). Example in JavaScript:

  ```javascript
function makeCounter (a) {
  var b = a;
  return function (c) {
    b += c;
    return b;
  }
}
var x = makeCounter(1);
x(2); //returns 3
x(3); //returns 6
makeCounter(1)(3); //returns 4
  ```

- **Lambda expression**: Most likely is an anonymous function, but not always. A shorter way to write functions. Comes from the concept of lambda calculus. \\( \lambda x.x^{2}  \\) is the lambda expression for the function  \\( f(x) = x^{2}  \\). Lambda is usable in a language because the functions are first class ([source](https://gist.github.com/ericelliott/414be9be82128443f6df)).


