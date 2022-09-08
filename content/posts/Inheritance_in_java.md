---
title: "Inheritance in java"
date: 2022-09-06T09:28:09+05:30
draft: false
tags: 
  - tech
  - java
---

In english inherit means to derive qualities from your ancestors gnetically.

Just like this in java also one class can inherit properties and methods of another class using inheritance. 


```java
Child extends Parent {

}

```

This  is the basic syntax for inheritance, We use extends keyword to inherit a class. The class that inherits is also called the subclass and the class which was inherited is called superclass.

To refer to parent class from child class we use super keyword and we need to construct parent in the child class before we intialize any of our properties in our constructor.


```java 
public ClassName() {
  super();
}
```

`super` is also used to refer to the parent. Assuming you have any method in super that you want acess to you would do it using super. It's not neccessary in all cases but it is good practice to use it to increase the readability of our code.


In java a class can only inherit one class. but multi level inheritance is still allowed.

Some classes may have similar methods doesn't mean inheritance is a great idea there a bird and a plane both can fly but one shouldn't inherit the other. To determine whether a class can inherit others you can use `is a`, if both classes have a `is a` realtionship.

Ex:- A lion is a cat.

So lion class can inherit cat class.


In general avoiding inheritance unless necessary is great practice. With inheritance you might want the banana but you will get the whole jungle.