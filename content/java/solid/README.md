# Solid Principle of Java

SOLID refers to five design principles in object-oriented programming, designed to reduce code rot and improve the value, function, and maintainability of software.

1. [Single Responsibility Principle](#single_responsibility_principle)
2. [Open Closed Principle](#open_closed_principle)
3. [Liskov Substitution Principle](#liskov_substitution_principle)
4. [Interface Segregation Principle](#interface_segregation_principle)
5. [Dependency Inversion Principle](#depedency_inversion_principle)



#### Single Responsibility Principle

The Single Responsibility Principle (SRP) states that there should never be more than one reason for a class to change. This means that every class, or similar structure, in your code should have only one job to do.

Everything in the class should be related to that single purpose. It does **not** mean that your classes should only contain one method or property.

There can be a lot of members as long as they relate to the single responsibility. It may be that when the one reason to change occurs, multiple members of the class may need modification. It may also be that multiple classes will require updates.



#### Open Closed Principle

The Open-Closed Principle (OCP) states that classes should be open for extension but closed for modification. “Open to extension” means that you should design your classes so that new functionality can be added as new requirements are generated. “Closed for modification” means that once you have developed a class you should never modify it, except to correct bugs.

Generally you achieve this by referring to abstractions for dependencies, such as interfaces or abstract classes, rather than using concrete classes. Functionality can be added by creating new classes that implement the interfaces.

Applying OCP to your projects limits the need to change source code once it has been written, tested, and debugged. This reduces the risk of introducing new bugs to existing code, leading to more robust software.



#### Liskov Substitution Principle

The Liskov Substitution Principle (LSP) was introduced by **Barbara Liskov**. It applies to inheritance in such a way that the **derived classes must be completely substitutable for their base classes**. In other words, if class A is a subtype of class B, then we should be able to replace B with A without interrupting the behavior of the program.

It extends the open-close principle and also focuses on the behavior of a superclass and its subtypes.



#### Interface Segregation Principle

The principle states that the larger interfaces split into smaller ones. Because the implementation classes use only the methods that are required. We should not force the client to use the methods that they do not want to use.

The goal of the interface segregation principle is similar to the single responsibility principle.



#### Dependency Inversion Principle

The principle states that we must use abstraction (abstract classes and interfaces) instead of concrete implementations. High-level modules should not depend on the low-level module but both should depend on the abstraction. Because the abstraction does not depend on detail but the detail depends on abstraction.
