---
layout: post
title: Strategy Pattern
categories: [CE,Design Pattern]
tags: [Design Pattern]
toc: true
date: 2021-09-08
---

## Strategy Pattern
According to *Head First: Design Pattern*, the defition of strategy pattern (策略模式) is 
> family of algorithms, encapsulated each one, and makes them interchangeable. Strategy lets the algorithm vary independently from cloents that use it.

<!-- more -->

Strategy Pattern is a [Behavioral Patterns]([isa-lai.com/w](https://isa-lai.com/wiki/#/software-development?id=type-of-design-patterns)).

## Principle
1. Take what varies or what might change and encapsulate(封装) it seperately.
2. Program to an interface, not an inplementation
3. Favor composition over inheritance, Has-a can be better than is-a.

Strategy Pattern encapsulates algotithm.

## Pros & Cons
Pros
1. Can easily change algorithm
2. Avoid using many judge (`if` statement)
3. Easily extantable

Cons
1. Need many stategy classes
2. All classes are expose to public

Strategy Pattern is suitable for when
1. Many classes only have difference in behavior. This pattern allow object dynamically choose behacior within the interface.
2. Dynamic algorithm
3. A class have many behavior. Using other pattern need many `if` statement.

## Build 
Context is a class using algorithm in stategy interface
![Strategy Pattern Class](https://www.runoob.com/wp-content/uploads/2014/08/strategy_pattern_uml_diagram.jpg)

### Interface
```java
public interface Strategy {
   public int doOperation(int num1, int num2);
}
```

### Class in interfave
```java
public class OperationAdd implements Strategy{
   @Override
   public int doOperation(int num1, int num2) {
      return num1 + num2;
   }
}
```
```java
public class OperationSubtract implements Strategy{
   @Override
   public int doOperation(int num1, int num2) {
      return num1 - num2;
   }
}
```
```java
public class OperationMultiply implements Strategy{
   @Override
   public int doOperation(int num1, int num2) {
      return num1 * num2;
   }
}
```

### Context
```java
public class Context {
   private Strategy strategy;
 
   public Context(Strategy strategy){
      this.strategy = strategy;
   }
 
   public int executeStrategy(int num1, int num2){
      return strategy.doOperation(num1, num2);
   }
}
```

### Implement
```java
public class StrategyPatternDemo {
   public static void main(String[] args) {
      Context context = new Context(new OperationAdd());    
      System.out.println("10 + 5 = " + context.executeStrategy(10, 5));
 
      context = new Context(new OperationSubtract());      
      System.out.println("10 - 5 = " + context.executeStrategy(10, 5));
 
      context = new Context(new OperationMultiply());    
      System.out.println("10 * 5 = " + context.executeStrategy(10, 5));
   }
}
```

Result:
10 + 5 = 15
10 - 5 = 5
10 * 5 = 50
