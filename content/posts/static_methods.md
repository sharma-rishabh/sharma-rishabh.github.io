---
title: "Static Methods"
date: 2022-08-25T08:27:47+05:30
draft: false
tags:
  - tech
---

# Static Methods in JavaScript

To understand static methods first we need to know what are normal methods of a
class.

## Normal Methods

All methods are defined and their reference is stored only once inside a class.


So how do all instances of class have access to that method?

What happens is that each instance first looks for which class it belongs to then it goes and looks for the method reference that was called upon and then we can think that the instance is sent as the first argument to that method but in  reality it is bound to that method so nobody needs to send it as an argument.


## Static Methods

It is easy to understand them now. They are declared at a class level so they're not bound with any instance so `this` inside them doesn't refer to any single instance of that class rather it refers to the whole class.


### Syntax

```js
class ClassWithStaticMethod() {
  static foo() {
    console.log('This is a static method.')
  }
}

ClassWithStaticMethod.foo();
```

A cool thing to try would be to check where does the `this` point in a normal method and where it points in a normal method.