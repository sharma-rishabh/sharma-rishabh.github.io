---
title: "Data types in java"
date: 2022-09-01T18:41:15+05:30
draft: false
tags:
  - tech
---

Java is a very strict language when it comes to types. If you want to do anything remotely complex you need to know what types are available.

For simply declaring a function you need to know what type you'll return and what types you'll accept beforehand which makes your life simple and complex at the same time.

It makes your life simple when you're writing the method but When you're trying to come up with it's signature you need to spend time to ensure you're defining it correctly.

Different data types in java are

- byte: Can hold 8 bit of signed two's compliment integer.
- short: Can hold upto 16 bit of signed two's compliment integer.
- int: Can hold upto 32 bit of signed two's compliment integer.
- long: Can hold upto 64 bit of signed two's compliment integer.
- float: Single precision 32 bit floating point.
- double: Double precision 64 bit floating point.
- boolean: It is used to hold only true or false value.
- char: Holds 16 bit unicode character.


Data types are very strict converting them from one to another is messy you have to do explicit type casting or they will be converted while you're performing any operation on them. Usually if they changed during an operation they will get promoted to a data type which occupies more memory or to a data type which is higher on the hierarchy like floats sits higher on the hierarchy than int and longs even though a long occupies more memory and can hold larger values.

Chars will be converted to int when any arithmatic operation on them is stored in and int it will yeild an int.
Char will be converted to its relative ascii value and then the arithmatic operation is performend on it.

If you're trying to do something like

```java
float a=1.2;
```
and the complier is throwing an error about lossy type conversion than you can explicitly add and f at the end of your floating point number.

```java
float a=1.2f;
```
Similar things apply for any other data type.

Using correct data types while writing codes will ensure that your code behaves as you expect it to behave.
If you think about the contract not just in terms of values but also types than it will make your code much cleaner and your contracts much stronger.

This is the main advantage for Java as it forces you to think about the contracts not just in terms of values but also in terms of types.

The compiler itself will make sure you're never violating a functions contract.