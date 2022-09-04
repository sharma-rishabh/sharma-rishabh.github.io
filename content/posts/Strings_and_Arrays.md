---
title: "Strings and Arrays"
date: 2022-09-04T16:51:04+05:30
draft: false
tags:
  - tech
  - java
---

## Strings

Strings are immutable and they don't change once defined.
String is a class in java which allows you to initialize a string literal.
String can be initialize in two different ways

- Declaring strings like a normal data type

  ```java
  String name = "some name";
  ```

- Initialializing a new class method.

  ```java
  String name = new String("some name");
  ```

String comes with various different methods like charAt, contains, replace, replaceAll, trim, split.
We cannot use indecies to access chars in a string because they are not iterable.

### String pool

String class hold a pool of already declared strings inside itself.
Whenever we declare a new string at first the string pool is checked if it already contains that string.
If it does than it gives the same reference back and doesn't initialize a new string.
If it doesn't than it initialize a new string literal and adds it to the string pool.

All this works really well because strings are immutable.

## Arrays

Arrays are a collection of homogenous data we can declare array in two ways 

### Basic syntax

```java
dataType[] variableName = dataType[size];
```
**OR**


```java
dataType[] variableName = {values};
```


if we declare and initalize the array it will be stored in the stack 

```java
int[] numbers = {1,2,3,4,5};
```

if we declare it only by giving the size it will be stored in heap.
```java
int[] numbers = int[5];
```


We can use a different for loop syntax to iterate over an array


```java
for(dataType element : arrayname) {
  System.out.println(element);
}
```