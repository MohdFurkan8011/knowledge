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
```sql
String query = """
    SELECT id, name
    FROM users
    WHERE active = true
    """;
```