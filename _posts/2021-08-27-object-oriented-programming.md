---
layout: post
title: Object-oriented Programming
subtitle: OOP of Java
categories: Java
tags: [Java,CS,OOP]
---

## What is OOP?

It is quite normal to be ask **"What is OOP"** in the interview. 
According to its definition in [Wikipedia](https://simple.wikipedia.org/wiki/Object-oriented_programming#:~:text=Object-oriented%20programming%20%28%20OOP%29%20is%20a%20way%20of,a%20certain%20way%2C%20which%20is%20called%20procedural%20programming.)

> Object-oriented programming (OOP) is a programming paradigm based on the concept of "objects", which can contain data and code: data in the form of fields (often known as attributes or properties), and code, in the form of procedures (often known as methods).

In short, an object has `fields` and `methods`. 

3 properties of an object:
- Behavior: method and process.
- State: how will it respond when calling the method.
- Identity: identify object with same behavior and state. 

## Class

The program use **Class** to **contruct** an **instance** of object.

Data stores in **instance field** and **method** is used to operate data.

### Relationship

3 Types of relationships
- Dependence: **uses-a**, method in A use the method in B
- Aggregation: **has-a**, A has object B
- Inheritance: **is-a**, A is a onject of B

### Encapsulation 封装
Protect the field. The field cannot be modified directly using assignment.

To Get & Set
- a **private** field
- a **public** acessor / getter
- a **public** settor

### Final
Set a fild to be **final** will require initialization in constructor. It cannot be modified later.(cannot set)
```java
class Emlpoyee
{
    private final String namd;
}
```

### Constructor
#### Overloading
Methods have same name but difference perameters.

## Static
> Static saves memory to make progrm memory efficient.

### Field
Every object of this class **shares the same** static field, whereas every object has its onw copy of non-static field.

When there is no object of this class, the static field still exist as it belong to class, not belong to object.

Every object can set value of this static field, so try not to use `public` if possible.

### Constant / Final
It can be call directly using class without contruct any instance.
```java
public class Math
{
    public static final double PI = 3.14...;
}
```
Call using
```java
Math.PI;
```

### Method
Call using class without instance.
```java
Math.pow(1,2);
```

## Parameter of Method
Call by
- value: passing value to method
- reference: passing address
- name: not used in java

### Call by Value
Java are mainly using **call by value**.
```java
public void triple(double x)
{
    //x will copy the value of parameter
    x*=3;
}
double init = 10;
triple(init); // init =10, x=30
```

### Call by Reference
To use call by reference, passing an object to parameter
```java
public void triple(Employee x)
{
    //x will be a copy of reference
    x.raiseSalary(3);
}
Employee init = new Employee(); // init is a reference of an instance
triple(init); // both x and init pointing to the same object
```

## Package
### import
Use * to import every class under a package. But cannot use `java.*` to import every package.
Static import allow using method without prename
```java
import java.util.*;
import static java.lang.System.*;

out.println("sample"); //System.out
```

### Construct
Use `package packagename` at the beginning. Make sure the file structure is the same as the index.
```java
package com.horstmann.corejave; //cd com/horstmann/corejave
public class Employee
{
    ..
}
```


