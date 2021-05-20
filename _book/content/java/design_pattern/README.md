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
  - [Proxy](#proxy)
- [Behavioral]()
  - [Chain of responsibility](#chain of responsibility)
  - [Command](#command)
  - [Iterator](#iterator)
  - [State](#state)



### Structural

#### Adapter

An adapter convert the interface of a class into another interface clients expect. It lets classes work 		  together that couldn’t otherwise because of incompatible interfaces.



#### Bridge

Bridge design pattern is used to decouple a class into two parts – *abstraction* and it’s *implementation* – so that both can evolve in future without affecting each other. It increases the loose coupling between class abstraction and it’s implementation.



#### Composite

Composite design pattern helps to compose the objects into tree structures to represent whole-part hierarchies. Composite lets clients treat individual objects and compositions of objects uniformly.

The composite pattern has four participates:

1. **Component**: provides default behavior for the interface common to all classes as appropriate.

2. **Leaf**: It represents leaf objects in the composition.

3. **Composite**: Composites stores child components and implements child related operations in the component interface.

4. **Client**: Client manipulates the objects in the composition through the component interface.

   

#### Decorator

Decorator design pattern is used to add additional features or behaviors to a particular instance of a class, while not modifying the other instances of same class.

“Wrapper” is the alternative nickname for the Decorator pattern that clearly expresses the main idea of the pattern. A *wrapper* is an object that can be linked with some *target* object. The wrapper contains the same set of methods as the target and delegates to it all requests it receives. However, the wrapper may alter the result by doing something either before or after it passes the request to the target.



#### Facade

Facade pattern hides the complexities of the system and provides an interface to the client using which the client can access the system. This type of design pattern comes under structural pattern as this pattern adds an interface to existing system to hide its complexities.

This pattern involves a single class which provides simplified methods required by client and delegates calls to methods of existing system classes.

A facade might provide limited functionality in comparison to working with the subsystem directly. However, it includes only those features that clients really care about.

When you call a shop to place a phone order, an operator is your facade to all services and departments of the shop. The operator provides you with a simple voice interface to the ordering system, payment gateways, and various delivery services.

#### Flyweight

Flyweight pattern is one of the [structural design patterns](https://www.geeksforgeeks.org/design-patterns-set-1-introduction/) as this pattern provides ways to decrease object count thus improving application required objects structure. Flyweight pattern is used when we need to create a large number of similar objects (say 105). One important feature of flyweight objects is that they are **immutable**. This means that they cannot be modified once they have been constructed.



#### Proxy

In proxy design pattern, a proxy object provide a surrogate or placeholder for another object to control access to it. Proxy is heavily used to implement lazy loading related use cases where we do not want to create full object until it is actually needed.

Proxies are generally divided into four types –

1. **Remote proxy** – represent a remotely located object. To talk with remote objects, the client need to do additional work on communication over network. A proxy object does this communication on behalf of original object and client focuses on real talk to do.
2. **Virtual proxy** – delay the creation and initialization of expensive objects until needed, where the objects are created on demand. Hibernate created proxy entities are example of virtual proxies.
3. **Protection proxy** – help to implement security over original object. They may check for access rights before method invocations and allow or deny access based on the conclusion.
4. **Smart Proxy** – performs additional housekeeping work when an object is accessed by a client. An example can be to check if the real object is locked before it is accessed to ensure that no other object can change it.



### Behavioral

#### Chain of responsibility

Chain of responsibility design pattern gives more than one object an opportunity to handle a request by linking receiving objects together in form of a chain.



#### Command

A Command Pattern says that "*encapsulate a request under an object as a command and pass it to invoker object. Invoker object looks for the appropriate object which can handle this command and pass the command to the corresponding object and that object executes the command*".



#### Iterator

Iterator pattern provides a way to access the elements of an aggregate object sequentially without exposing its underlying representation.



##### Mediator

**Mediator** is a behavioral design pattern that lets you reduce chaotic dependencies between objects. The pattern restricts direct communications between the objects and forces them to collaborate only via a mediator object.



##### Memento

**Memento** is a behavioral design pattern that lets you save and restore the previous state of an object without revealing the details of its implementation.



##### Observer

**Observer** is a behavioral design pattern that lets you define a subscription mechanism to notify multiple objects about any events that happen to the object they’re observing.



#### State

In state pattern allows an object to alter its behavior when its internal state changes. The object will appear to change its class. There shall be a separate concrete class per possible state of an object.