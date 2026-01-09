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

#### Garbage Collector

Before Java 15:

- Some modern GCs existed
- But they were experimental
- Risky to use in production

In Java 15:
✅ These GCs became stable and production-ready
✅ Safer to use in real applications
✅ Better performance and predictability

***Comparison with Traditional GCs***
| GC Type | Pause Time | Heap Size Handling | Java 15 Status |
|---------|------------|--------------------|----------------|
| Serial GC | High | Small heaps | Stable |
| Parallel GC | Medium–High | Medium heaps | Stable |
| G1 GC (default) | Low–Medium | Large heaps | Stable |
| ZGC | Very Low | Huge heaps | Production |
| Shenandoah | Very Low | Huge heaps | Production |


#### EdDSA

1. What Is EdDSA? (In Simple Words)

- EdDSA is a modern digital signature algorithm used to:
- Prove who sent a message
- Ensure the message was not changed
- Provide strong security with high performance

👉 Think of it as a very fast, very secure digital signature.

2. Why Do We Need Digital Signatures?

Digital signatures are used for:
- HTTPS / TLS
- JWT tokens
- Software updates
- API authentication
- Blockchain and crypto systems

They guarantee:
- Authenticity
- Integrity
- Non-repudiation

3. Why EdDSA Is Important (Compared to Older Algorithms)

***Older Algorithms***
- RSA
- DSA
- ECDSA

***Problems with Older Ones***

- Slower
- More complex
- Easy to misuse

Some depend on random numbers (which can be risky)

4.  What Makes EdDSA Special?

Key Advantages
i. Very Fast
- Faster than RSA and ECDSA
- Great for high-throughput systems

ii. Very Secure
- Based on Edwards elliptic curves
- Strong resistance to common attacks

iii. Deterministic
- Does not rely on random numbers during signing
- Avoids bugs that broke ECDSA in the past

iv. Simple & Safe API
- Harder to misuse
- Fewer configuration mistakes

```java
KeyPairGenerator kpg = KeyPairGenerator.getInstance("Ed25519");
KeyPair kp = kpg.generateKeyPair();
```

| Feature | RSA | EdDSA |
|--------|-----|-------|
| Speed | Slow | Very fast |
| Key size | Large | Small |
| Security | Good | Excellent |
| Randomness dependency | Yes | No |