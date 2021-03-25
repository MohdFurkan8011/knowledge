# Collection

A Collection is a group of individual objects represented as a single unit. Java provides Collection Framework which defines several classes and interfaces to represent a group of objects as a single unit.

The Collection interface (**java.util.Collection**) and Map interface (**java.util.Map**) are the two main “root” interfaces of Java collection classes.

**Need for Collection Framework :**
Before Collection Framework (or before JDK 1.2) was introduced, the standard methods for grouping Java objects (or collections) were Array or Vector or Hashtable. All of these collections had no common interface.

1. [Collection]()
2. [List](List/List.md)
3. [Set](Set/Set.md)
4. [Map](Map/Map.md)
5. [Queue](Queue/Queue.md)
6. [Deque](Deque/Deque.md)

- Dictionary - It is an abstract class which is implemented by Hashtable and Property class, which provide key-value storage repository and operated much like Map.
- Hashtable - The Hashtable class implements a hash table, which maps keys to values. Any non null object can be used as key or as a value. It must implement the hasCode() and the equals() method. The initial default capacity of HashTable class is 11 whereas load factor is 0.75. It is thread safe.
- 