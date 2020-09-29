---
layout: post
title: Commonly Asked OOP Question
tags: [Coding Interview]
---

## What is Encapsulation? 

Encapsulation can mean one of two things:

1. Hide data/Restrict access to data by adding appropriate modifiers (private or protected) to members of an object.
2. Bundling data/fields (object state) and methods (object behavior) together. Operations (modifications or data extractions) on the data are done through appropriate setter/getter methods.

### Why do we need encapsulation?

1. ***Re-usability***: The underlying implementation / internal state is hidden from outside classes/users. So the implementation can be changed at any point without breaking the classes that use the code. This increases maintainability.

2. ***Flexibility, Tighter control and Security***: Different levels of control for the class members are possible. For example, if we wish to make a field read-only, then we can specify only the getter method for that field. This ensures that there is no way for an outside class to modify the value of that field. (Although there are other ways to achieve this, e.g., using ``final`` in Java or ``const`` in C++). Also we have more control over implementation. For example, we can add checks/conditions/throw exceptions when some value needs to be updated. From a security standpoint, this reduces the [attack surface](https://en.wikipedia.org/wiki/Attack_surface). 

3. ***Implementation is hidden*** from the users/outside classes. This increases modularity.

[This answer](https://stackoverflow.com/a/25752613/5672613) explains how encapsulation reduces the dependencies between modules. 

## Encapsulation vs Abstraction

In simple terms:

- ***Encapsulation***: Hiding information (Concrete)
- ***Abstraction***: Hiding implementation (Abstract, Focus on what instead of how)

Abstraction is the process of generalization. Abstraction provides an interface to the users for interaction. For example, a mobile phone may have complex logic inside a circuit board encapsulated, and provides a user interface to the users to interact with the phone. Another example of encapsulation: Encapsulating necessary information on different layers of OSI model (Networking). Each layer encapsulates the data of higher layers inside header (more specifically, inside PDUs (Protocol Data Units)).

[This post](https://stackoverflow.com/q/742341/5672613) contains several useful answer describing the differences between abstraction and encapsulation.

### What is Polymorphism?

Poly means many and morph means figure or shape. So polymorphism means the ability to take on multiple figure/shapes. The base class/parent class can take on the form of different sub-class/child class. Polymorphism is achieved via abstract classes (C++, Java) or interfaces (Java). For example, we can have a class ``Car``. Now every car has a some number seats. Now a ``get_seats()`` function would not be definable for ``Car`` class simply because there is no common number of seats for every car. So each car (e.g., private car, truck, bus, sports car etc.) inherits from the ``Car`` class an abstract function ``get_seats()`` and takes the responsibility to implement it. Now for each specific instance, we can call ``get_seats()`` and get the different number of seats.  This saves us from writing separate function for each car instance, e.g., ``get_private_car_seats()``, ``get_bus_seats()`` etc. 

### Why do we need Polymorphism?   
   
1. Polymorphism allows for single interface and multiple implementations. 
2. Reduces code complexity.

Polymorphism can be achieved in two ways:

1. ***Compile time polymorphism***
    - Function overloading: Multiple function with same name but different type/number of parameters and/or return types
    - Operator overloading: Overload same operator for different classes. For example string concatenation or adding complex numbers

2. ***Runtime polymorphism***
    - Function overriding: Change definition of function inside derive/sub-class/child class. E.g., Java's ``toString()`` function. 


### Why do we need Inheritance?

1. Enabling code reuse.
2. Extend existing functionality instead of starting from scratch.

Java allows multilevel inheritance and C++ allows multiple inheritance. But you may run into [The Diamond Problem](https://en.wikipedia.org/wiki/Multiple_inheritance#The_diamond_problem) if multiple inheritance is implemented with care.

We can use ``interface`` in Java to achieve the functionality of multiple inheritance. 

Question: How does ``interface`` solve Diamond problem?

***To be continued***: Composition over Inheritance, Circle-ellipse problem, Liskov Substitution Principle 


