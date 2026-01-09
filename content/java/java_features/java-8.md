### Java 8



#### Java 8 Features

- [Date Time](#date-time)
- [Lambda Expressions](#lambda-expressions)
- [Functional Interface](#functional-interface)
- [Method Reference](#method-reference)
- [Stream](#stream)
- Collectors
- Spliterator
- Default Method
- forEach Method
- String Joiner
- [Optional Class](#optional-class)
- Type Inference
- [HashMap Changing](#hashmap-changing)



#### Date Time

The java.time, java.util, java.sql and java.text packages contains classes for representing data and time.

Java has introduced a new Date and Time API since java 8. The java.time package contains java 8 date and time classes.

`LocalDate, LocalTime, LocalDateTime, MonthDay, OffsetTime, OffsetDateTime, Clock, Year, YearMonth, Period, Duration, DayOfWeek enum, Month`



#### Lambda Expressions

Lambda Expression is an anonymous function which accepts a set of input parameters and returns results.

Lambda Expression is a block of code without any name, with or without parameters and with or without results. This block of code is executed on demand. It has three part, parameter, arrow operator, expression body.

() -> parameter

parameter -> expression

(parameter1, parameter 2) -> expression

(parameter1, parameter 2) -> { code block)

> Benefit of lambda expression
>
> 1. Fewer line of code
> 2. Sequential and Parallel execution support by passing behavior in methods.



#### Functional Interface

An interface with exactly one abstract method is called Functional interface. ``@FunctionalInterface`` annotation is added so that we can mark an interface as functional interface.

It is not mandatory to use it, but it is best practice to use it with functional interface to avoid addition of extra methods accidentally. If the interface is annotation with ``@FunctionalInterface`` annotation and we try to have more than one abstract method, it throws compile error.

```java
The major benefit of java 8 functional interface is that we can use lambda expressions to instantiate them to avoid using bulky anonymous class implementation.
```

Steam API is introduced that uses a lot of functional interface.

java.util.function has build in functional interfaces.

- **Consumer<T>** -  Represents an operation that accepts a single input argument and returns no result.

  It has two methods,

  ```
  void accept(T t) - Performs operation on the given argument
  
  default Consumer<T> andThen(Consumer<? super T> after) - return a composed Consumer that performs, in sequence, this operation followed by the after operation
  ```

  Others interfaces - BiConsumer<T,U>, DoubleConsumer, IntConsumer, LongConsumer, ObjDoubleConsumer<.T>, ObjIntConsumer<T>, ObjLongConsumer<T>

  

- **Supplier<T>** - takes no argument and returns output.

  It has one methods

  ```
  T get()
  ```

  

- **Function<T,R>** - Represents a function that accepts one argument and produces a result.

  It has following methods

  ```
  andThen(Function f)
  apply(T t)
  compose(Function f)
  identify()
  ```

  Others interfaces - BiFunction, DoubleFunction, DoubleToIntFunction, DoubleToLongFunction etc.

- **Predicate<T>** - Represents a predicate (boolean valued function) of one argument.

  It has following methods

  ```
  and(Predicate p)
  or(Predicate p)
  isEquals(Object target)
  test(T t)
  ```

  Others interfaces - BiPredicate, DoublePredicate, IntPredicate, LongPredicate

- **BinaryOperator<T>** - Represents an operation upon two operands of the same type, producing a result of the same type as the operand. It also extends BiFunction.

  ```
  maxBy(Comparator c)
  minBy(Comparator c)
  ```

  Other interfaces - DoubleBinaryOperator, IntBinaryOperator, LongBinaryOperator



#### Method Reference

Method reference is used to refer method of functional interface. Each time when you are using lambda expression to just referring a method, you can replace your lambda expression with method reference.

*Type of method reference*

1. Reference to a static method
2. Reference to an instance method
3. Reference to a constructor



#### Stream

A stream is a sequence of objects that supports various methods which can be pipelined to produce the desired result.

The steam API is used to process collections of objects.

- A stream is not a data structure instead it takes input from the collections.
- Stream does not change original data structure
- Each intermediate operation is lazily executed and returns a stream as a result, hence various intermediate operations can be pipelined. Terminal operations mark the end of the stream and return the result.

***Intermediate operations***

​	filter(), map(), flatMap(), sorted(), peek(), limit(), skip()

***Terminal operations***

​	allMatch(), anyMatch(), noneMatch(), collect(), count(), forEach(), min(), max(), reduce(), findFirst(), findAny()

map() transforms data, where flatMap() is a combination of a map and a flat operation.



#### HashMap Changing

HashMap performance Improvement Changes in Java 8, The Oracle made this change in HashMap due to performance factor. 

Earlier before Java 8, the performance of the *HashMap* was poor due to the hash collision, it degrades the performance of HashMap significantly. This change can be notifiable only when if you are using the HashMap for a large number of elements, *why (see below points)?*

The traversal of *HashMap,* get(), and other methods lookup time of *HashMap* have a negative impact due to hash collisions. This situation you can face when multiple keys end up in the same bucket, then values along with their keys are placed in a linked list. So, the retrieval time of elements from HashMap increases from ***O(1)*** to ***O(n)***. Because the linked list has to be traversed to get the entry in the worst case scenario.

But **Java 8** has come with the following new strategy for *HashMap* objects in case of high collisions.

- To address this issue, Java 8 hash elements use **balanced trees instead of linked lists** after a certain **threshold** is reached. Which means HashMap starts with storing Entry objects in a linked list but after the number of items in a hash becomes larger than a certain threshold. The hash will change from using a linked list to a balanced tree.

