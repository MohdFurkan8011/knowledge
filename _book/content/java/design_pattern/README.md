# Design Pattern

Design patterns represent the best practices used by experienced object-oriented software developers. Design patterns are solutions to general problems that software developers faced during software development.

Design patterns can speed up the development process by providing tested, proven development paradigms. Effective software design requires considering issues that may not become visible until later in the implementation.

- [Creational](creational/README.md)
  - [Singleton](creational/Singleton.md)
  - [Prototype](creational/Prototype.md)
  - [Factory](creational/Factory.md)
  - [Abstract Factory](creational/Abstract_Factory.md)
  - [Builder](creational/Builder.md)
  - [Object Pool](creational/Object_Pool.md)
- [Structural](#structural)
  - [Adapter](#adapter)
  - [Bridge](#bridge)
  - [Composite](#composite)
  - [Decorator](#decorator)
  - [Facade](#facade)
  - [Flyweight](#flyweight)
  - [Proxy]()
- [Behavioral]()
  - [Chain of responsibility]()
  - [Command]()
  - [Interpreter]()
  - [Iterator]()
  - [Mediator]()
  - [State]()
  - [Strategy]()
  - [Template Method]()
  - [Visitor]()



#### Structural

##### Adapter

An adapter convert the interface of a class into another interface clients expect. It lets classes work 		  together that couldn’t otherwise because of incompatible interfaces.



##### Bridge

Bridge design pattern is used to decouple a class into two parts – *abstraction* and it’s *implementation* – so that both can evolve in future without affecting each other. It increases the loose coupling between class abstraction and it’s implementation.



##### Composite

Composite design pattern helps to compose the objects into tree structures to represent whole-part hierarchies. Composite lets clients treat individual objects and compositions of objects uniformly.



##### Decorator

Decorator design pattern is used to add additional features or behaviors to a particular instance of a class, while not modifying the other instances of same class.



##### Facade

The facade pattern is appropriate when you have a **complex system** that you want to expose to clients in a simplified way, or you want to make an external communication layer over an existing system which is incompatible with the system. Facade deals with interfaces, not implementation. Its purpose is to hide internal complexity behind a single interface that appears simple on the outside.



##### Flyweight

Flyweight pattern is one of the [structural design patterns](https://www.geeksforgeeks.org/design-patterns-set-1-introduction/) as this pattern provides ways to decrease object count thus improving application required objects structure. Flyweight pattern is used when we need to create a large number of similar objects (say 105). One important feature of flyweight objects is that they are **immutable**. This means that they cannot be modified once they have been constructed.

