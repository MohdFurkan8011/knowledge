### Java 15

#### New features

- [Text Blocks](#text-blocks)
- [Sealed Classes](#sealed-classes)
- [Records](#records)
- [Pattern Matching](#pattern-matching)
- [Hidden Classes](#hidden-classes)
- [Garbage Collector](#garbage-collector)
- [EdDSA](#EdDSA)
- [Nashorn JavaScript Engine](#nashorn-javascript-engine)


#### Text Blocks
***Why it matters***: Greatly improves code readability and maintainability.
Allows multi-line strings using """.
Ideal for SQL, JSON, XML, HTML, and large text.
Eliminates excessive escaping and string concatenation.
```java
String query = """
    SELECT id, name
    FROM users
    WHERE active = true
    """;
```


#### Sealed Classes
***Why it matters:*** Better domain modeling and safer inheritance.
Limits which classes can extend or implement a type.
Helps enforce business rules at compile time.
Works well with pattern matching.
```java
public sealed interface Shape
    permits Circle, Rectangle {}
```


#### Records
***Why it matters:*** Dramatically reduces boilerplate for data classes.
Perfect for DTOs, value objects, API responses, and configuration models.
Automatically generates constructor, getters, equals, hashCode, and toString.
```java
public record User(String name, int age) {}
```


#### Pattern Matching
***Why it matters:*** Reduces boilerplate and makes conditional logic cleaner.
Combines type checking and casting in one step.
Makes code safer and more readable.
```java
// previous version
Object obj = "Hello";
if (obj instanceof String) {
    String s = (String) obj;   // explicit cast required
    System.out.println(s.length());
}

// java 15    no explicit cast
if (obj instanceof String s) {
    System.out.println(s.toUpperCase());
}
```


#### Hidden Classes
***1. What Problem Do Hidden Classes Solve?***
Some Java frameworks generate classes at runtime, for example:
- Spring (proxies)
- Hibernate (lazy-loading entities)
- Mockito (mock objects)
- ByteBuddy / ASM (bytecode generation)

Before Java 15

Generated classes:
- Had names
- Were loaded into the class loader
- Stayed in memory for a long time
- Could accidentally be referenced

This caused:
❌ Memory leaks
❌ Classloader pollution
❌ Slower startup
❌ Harder GC cleanup

***2. What Is a Hidden Class?***

A Hidden Class is:
- A class created at runtime
- Not discoverable by name
- Not loadable by other classes
- Strongly encapsulated
- Garbage-collectable when no longer used

💡 Think of it like a temporary anonymous class that exists only for internal use.

***3. Simple Analogy 🧠***
***Normal Class***
- Like a named employee:
- Has an ID
- Listed in company records
- Can be contacted by others

***Hidden Class***
- Like a temporary contractor:
- No public ID
- Only known to the manager who hired them
- Disappears when the job is done

***You care ONLY IF you are:***

- Writing a framework
- Generating bytecode at runtime
- Building proxies, mocks, or DSLs
- Working on JVM tooling