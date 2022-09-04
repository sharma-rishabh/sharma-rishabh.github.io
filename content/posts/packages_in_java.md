---
title: "Packages in Java"
date: 2022-09-04T16:45:47+05:30
draft: false
tags: 
  - tech
  - java
---

## Package

A package is a grouping of related types providing access protection and name space management.

## Advantages

- Easy to determine how types are related.
- Makes sure that your names don't conflict with the names used in the package.


## Creating a package

```java
import mypackage;
```

## Naming Convention 

Packages solve the naming problem but what if two programmers create packages with the same name. That's why we have naming convention for packages.

- Package names are written in all lowercase.
- Companies use their reverse domain name to begin their project 
  - ex: com.example.package
- If multiple package with similar name are there in the company then project name can be added to package name.
  - ex: com.example.project.package


## Package Members

The types that comprise of a package are called package members.


## Fully qualified name

A fully qualified name of a package member is the package name followed by the type you want to access.

```java
com.example.project.mypackage.ClassName
```


## Using package members



### Refering using fully qaulified name.

If you have not imported a package than you can access the types defined in that package by using their fully qualified name.



### Importing a package member

You can import the specific memebers of a package using import statement.

```java
import com.example.project.mypackage.ClassName;
```

Now you don't need to use the fully qualified name to use this package member.



### Importing a whole package

You can import the whole package and access all it's type using simple names instead of full qualified names.


```java
import com.example.project.mypackage.*;
```



For convinience complier automatically imports two packages for all source files java.lang and the current package.


All Classes and variables by default have package scope if we don't use `public` or `private`.



