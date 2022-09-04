---
title: "Method overloading in java"
date: 2022-09-04T16:33:47+05:30
draft: false
tags: 
  - tech
  - java
---

Method overloading is the process of having mulitple method defination with a single name.
The complier knows which one to call on the basis of the signature of the method which ever signature matches the call that method is invoked.

By default while overloading if the contract doesn't match it tries to type convert and see if any siganture match like you can have a method to add two ints and if you try to call it with chars it will get invoked.

The type conversion is only done if it is not lossy if you have a method that adds two bytes and you try to call it with chars it won't get invoked since it is a lossy conversion to convert chars to bytes.

You can also overload static methods.
