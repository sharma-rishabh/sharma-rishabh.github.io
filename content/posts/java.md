---
title: "Starting With Java"
date: 2022-09-01T18:26:43+05:30
draft: false
tags:
  - tech
---

Java is a type specific language which is a lot stricter than javascript.

Let's follow the journey of java code.

First Java code is compiled into byte code by a compiler. Byte code is highly optimised so the code can be run quickly by JVM Java Virtual Machine. JVM combined with some System Library make a JRE Java Run Time Environment. The compiler and the JRE together make JDK Java Development Kit.

## Set up JDK

```sh
brew tap adoptopenjdk/openjdk
brew install --cask adoptopenjdk8
```

Run these two commands on your shell to setup JDK on your machine.



Let's start writting Java code now you can write whatever code you want to write.

## Example

```java
class Example {
  public static void main(String [] args) {
    System.out.println("Hello World");
  }
}
```

Make sure to follow convention and give your file the same name as your class.

Compile your file

```sh
javac FileName.java
```

After compiling your code you will see that you have a .class file with the same name as your file
then you can run the code by running.

```sh
java ClassName
```

This should get set you up so you can start writing more complex things.
