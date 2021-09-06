---
layout: post
title: Inheritance (1) - Base
subtitle: Basic Inheritance in Java
categories: Java
tags: [Java,CS,OOP]
---

Inheritance is an importance concept in OOP. This article is based on Java Object-oriented Programming. 

## Type of Class
- Supper Class 超类
- Base Class 基类
- Parent Class 父类
- Subclass 子类
- Derived Class 派生类
- Child Class 孩子类、

In Java, using `extends` to inheritance. In this case, **Manager** is the subclass of super class **Employee**.
```java
public class Manager extends Employee
{
    ...
}
```
SUbclass will have the properties and methods in parent class, so it generally have more preperties and methods than parent. Subclass cannot directly access to the private field of super class.

To access the super class, use `super`
```java
double baseSalary = super.getSalary();
```
In C++, using `::`
```cpp
double baseSalary = Employee::getSalary();
```

## Construct a Subclass
```java
public Manager(String name,double salary,int year,int month,int day)
{
    super(name,salary,year,month,day)
    bonus=0;
}
```
In this case, the field in superclass `Employee` is private, so it need `super()` to initiate the values. If it does not have `super()` constructor. It automatically call the default constructor in super class(which does not have parameter). It the default constructor not exist, compiler will output wrong message.  

## Polymorphism
According to [techopedia](https://www.techopedia.com/definition/28106/polymorphism-general-programming#:~:text=Definition%20-%20What%20does%20Polymorphism%20mean%3F%20Polymorphism%20is,the%20general%20rather%20than%20program%20in%20the%20specific.)
> Polymorphism is an object-oriented programming concept that refers to the ability of a variable, function or object to take on multiple forms. A language that features polymorphism allows developers to program in the general rather than program in the specific.

For example, **Employee** can use any subcloss like **Manager** and **Secretary**. 
```java
Manager boss = new Manager();
Employee[] staff = new Employee[3];
staff[0] = boss;
```
Even `staff[0]` and `boss` point to the same instance. Compiler see `staff[0]` as a Employee. 

### Static & Dynamic Bind Method
- Static: private static final
- Dynamic: method called depend on the **parameters**. The JNM search in all method to find the correct one, which cost running time. 

## Final
When method or properties is `final`, the subclass cannot override it. 