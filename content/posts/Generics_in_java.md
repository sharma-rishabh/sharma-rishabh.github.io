---
title: "Generics in java"
date: 2022-09-12T21:00:55+05:30
draft: false
tags:
  - tech
  - java
---

Generics in java are used to specify a type which would be known only when the code is ran or called not when it is written.

Generic also helps you to write code that can work with wide variety of types. So you don't need to overload a function uneccesarily.

## Syntax for classes

```java
class Box<T> {

}

class Pencil {

}

// Class creation

Box<Pencil> = new Box<Pencil>();
```

In the example above we are creating a generic class and we are telling a type `T` will be given at call time in the example above we created a class Box and at call time we provided a class Pencil. The syntax above will be read as a Box of Pencil a Box of Pencil is a type initself and Unique instances of it be created and a Box of Something will have no relation with the box of pencil. 

```java
T c = new T();
```
This line will be equivalent to 

```java
Pencil c = new Pencil()
```

Since we said that will be equivalent to Pencil at call time.

One thing to note is that this won't make all the methods of pencil available inside box rather only Object methods will be available here. In byte code also T will equate to Object.
You might be thinking why not use Object directly. Generics are used to Provide compile time safety. Java is a compiled language and if we use it's type systems correctly we can catch most of the bugs at compile time rather that run time. Generics help us take full advantage of java's compile cycle whereas Object will just leave us with bugs which could've been caught at complie time.One more reason to use Generics is that you can always type cast them.
