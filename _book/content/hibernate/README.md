# Hibernate

- [Hibernate QA](#hibernate qa)

#### Hibernate QA

**Q1. What is hibernate in java?**

**Ans:** Hibernate ORM (Hibernate in short) is an object-relational mapping tool for the Java programming language. It provides a framework for mapping an object-oriented domain model to a relational database. Hibernate also provides data query and retrieval facilities.

**Q2. Is hibernate better than JDBC?** 

**Ans:** JDBC will always give better performance as compared to Hibernate for most of the database vendors.  The choice of hibernate over jdbc and sql queries is not because of the performance but because of reasons mainly object persistence and database independence in terms of not writing database specific queries.

**Q3. Why do we need hibernate in Java?**

**Ans:** So with JDBC, mapping between Java objects and database tables is done manually. Hibernate reduces lines of code by maintaining object-table mapping itself and returns result to application in form of Java objects. Hibernate, with Transparent Persistence, cache is set to application work space.

**Q4. What is the use of ORM in Java?**

**Ans:** ORM allows you to use java objects as representation of a relational database. It maps the two concepts (object-oriented and relational) Hibernate is an ORM framework – you describe how your objects are represented in your database.

**Q5. What is the difference between JPA and Hibernate?**

**Ans:** JPA is the interface, Hibernate is one implementation of that interface. JPA is a specification for accessing, persisting and managing the data between Java objects and the relational database. As the definition says its API, it is only the specification. Hibernate is a JPA provider.

**Q6. What is the use of Session in hibernate?**

**Ans: ** The main runtime interface between a Java application and Hibernate. It provides method for managing data ex. save, update, delete etc.

There are three way to get session object in hibernate.

openSession(), getCurrentSession(), openStatelessSession(), these methods of SessionFactory class

**Q7. Can we use only JPA without hibernate?**

**Ans:** you can't use JPA on its own. JPA is a specification, which defines an API for object-relational mappings and for managing persistent objects and you need a JPA provider to implement it, like Hibernate, EclipseLink.

**Q8. What are the fetching strategies supported by hibernate?**

**Ans:** 

* Join fetching, 
* Select fetching, 
* Subselect fetching, 
* Batch fetching, 
* Immediate fetching, 
* Lazy collection fetching, 
* Proxy fetching

**Q9. What is a polymorphic association?**

**Ans:** A relationship from one class to multiple classes.

**Q10. What is the difference between session and Sessionfactory in hibernate?**

**Ans:** SessionFactory is Hibernate’s concept of a single datastore and is threadsafe so that many threads can access it concurrently and request for sessions and immutable cache of compiled mappings for a single database. Sessions are opened by a SessionFactory and then are closed when all work is complete.

**Q11. What is the difference between load and get method in hibernate?**

**Ans:** Session.load(): It will always return a “proxy” (Hibernate term) without hitting the database. In Hibernate, proxy is an object with the given identifier value, its properties are not initialized yet, it just look like a temporary fake object. If no row found , it will throws an ObjectNotFoundException.

Session.get() loads instance immediatelly, If no row found returns null.

**Q12. Is hibernate Sessionfactory Singleton?** 

**Ans:** Session factory objects are to be implemented using the **singleton** design pattern. Instances of SessionFactory are *thread-safe* and typically shared throughout an application. As these objects are heavy weight because they contains the connection information, hibernate configuration information and mapping files,location path. So creating number of instances will make our application *heavy weight*. But the session objects are not thread safe. So in short it is - SessionFactory objects are one per application and Session objects are one per client.

**Q13. What are the configuration files in hibernate?**

**Ans:** Hibernate also requires a set of configuration settings related to database and other related parameters. All such information is usually supplied as a standard Java properties file called hibernate.properties, or as an XML file named hibernate.cfg.xml.

We do need configuration xml files in case of annotation.

**Q14. What is the use of dialect in hibernate?**

**Ans:** Dialect means “the variant of a language”. Hibernate, as we know, is database agnostic. It can work with different databases. However, databases have proprietary extensions/native SQL variations, and set/sub-set of SQL standard implementations. Therefore at some point hibernate has to use database specific SQL.

**Q15. What is the use of Show_sql in hibernate?**

**Ans:** Hibernate has build-in a function to enable the logging of all the generated SQL statements to the console. You can enable it by add a “show_sql” property in the Hibernate configuration file “ hibernate.cfg.xml “.

**Q16. What is hibernate proxy and how it helps in lazy loading?**

**Ans:** A proxy is a subclass implemented at runtime. Hibernate creates a proxy (a subclass of the class being fetched) instead of querying the database directly, and this proxy will load the “real” object from the database whenever one of its methods is called.

**Q17. Is session is thread safe in hibernate?**

**Ans:** Session is not thread safe in hibernate.

**Q18. What is the use of configuration in hibernate?**

**Ans: ** The org.hibernate.cfg.Configuration is used to build an immutable org.hibernate.SessionFactory . The mappings are compiled from various XML mapping files. A org.hibernate.cfg.Configuration also allows you to specify configuration properties.

**Q19. What is criteria in hibernate?**

**Ans:** In Hibernate, the Criteria API helps us build criteria query objects dynamically. Criteria is a another technique of data retrieval apart from HQL and native SQL queries. 

**Q20. What is the difference between lazy and eager loading in hibernate?**

**Ans:** All data is fetched when eager marked data in the object when session is connected. However, in case of lazy loading strategy, lazy loading marked object does not retrieve data if session is disconnected (after session.close() statement). All that can be made by hibernate proxy.

**Q21. Is Sessionfactory immutable?**

**Ans:** The internal state of a SessionFactory is immutable. Most problems with concurrency occur due to sharing of objects with mutable state. Once the object is immutable, its internal state is setted on creation and cannot be changed. So many threads can access it concurrently and request for sessions.

**Q22. Is Hibernate configuration file mandatory?**

**Ans:** Basically you are setting all the required properties via your properties object so there is no real need to tell Hibernate to look for a hibernate.cfg.xml file which is exactly what the configure() method does. No, it’s not mandatory to use hibernate.cfg.xml. Just don’t use .configure().

**Q23. What is meant by annotation in hibernate?**

**Ans:** Hibernate annotations are the way to define mappings without the use of XML file. You can use annotations in addition to or as a replacement of XML mapping metadata.

**Q24. What does hibernate.hbm2ddl.auto create means?**

**Ans:** hibernate.hbm2ddl.auto. Automatically validates or exports schema DDL to the database when the SessionFactory is created. With create-drop , the database schema will be dropped when the SessionFactory is closed explicitly.

**Q25. What is the meaning of persistence in hibernate?**

**Ans:** When a POJO instance is in session scope, it is said to be persistent i.e hibernate detects any changes made to that object and synchronizes it with database when we close or flush the session.

**Q26. What is first level cache in hibernate?**

**Ans:** First level cache is associated with “session” object. The scope of cache objects is of session. First level cache is enabled by default and you can not disable it. When we query an entity first time, it is retrieved from database and stored in first level cache associated with hibernate session.

If we ask again same object which is in cache, it give object from cache, it does not hit database again.

**Q27. What is the use of Session in hibernate?**

**Ans:** Session is one main interface of hibernate, which provides method for managing data also transaction  methods.

**Q28. What is in HQL?**

**Ans:** Hibernate Query Language (HQL) is an object-oriented query language, similar to SQL, but instead of operating on tables and columns, HQL works with persistent objects and their properties.

**Q29. What is the use of projection in hibernate?**

**Ans:** Hibernate Projections are used in order to query only a subset of the attributes of an entity or group of entities you’re querying with Criteria.

**Q30. What are the different cascade types in hibernate?**

**Ans:** 

**Q31. Can I disable first level cache in hibernate?**

**Ans:** No,

**Q32. What is the use of bag in hibernate?** 

**Ans:** Hibernate Bag is a java collection that stores elements without caring about the sequencing, but allow duplicate elements in the list. A bag is a random grouping of the objects in the list.

**Q33. What is the use of Mappedby in hibernate?**

**Ans:** With the mappedBy , you directly tell Hibernate/JPA that one table owns the relationship, and therefore it is stored as a column of that table.

**Q34. What is inverse true in hibernate?**

**Ans:** The real meaning is that it defines which side is the parent or the relationship owner for the two entities (parent or child). Hence, inverse=”true” in a [Hibernate mapping](https://github.com/hibernate/hibernate-orm) shows that this class (the one with this XML definition) is the relationship owner; while the other class is the child.

**Q35. What is a bidirectional relationship?** 

**Ans:** In a bidirectional relationship, each entity has a relationship field or property that refers to the other entity. Through the relationship field or property, an entity class’s code can access its related object.

**Q36. What is the dirty checking in hibernate?**

**Ans:** Hibernate allows dirty checking feature.All persistent objects are monitored by hibernate.it detects which objects have been modified and then calls update statements on all updated objects.the process of updating the changed object is called automatic dirty checking.

**Q37. What are the important interfaces in hibernate?**

**Ans:** Configuration, SessionFactory, Session, Query, Criteria, Transaction

**Q38. What is difference between openSession() and getCurrentSession()?**

**Ans:** SessionFactory.openSession() always opens a new session that you have to close once you are done with the operations.

SessionFactory.getCurrentSession() returns a session bound to a context – you don’t need to close this.

**Q39. What are different states of an entity bean in Hybernate?**

**Ans:** Transient: When ever we create a new object of Entity bean then we can say that is in Transient state,At that time any modification in the object state does not effect on database.

Persistent: When ever the Object of entity bean associated with session we can say that is in persistent state, if any change in the object state , then that modification effects in database.

Detached :When ever the object is removed from session then it enters in to detached state.Any modification on detached state object , does not effect in database.

**Q40. Difference between hibernate session merge() vs update()?** 

**Ans:** Update: if you are sure that the session does not contains an already persistent instance with the same identifier,then use update to save the data in hibernate

Merge: if you want to save your modifications at any time with out knowing about the state of an session, then use merge() in hibernate.

**Q41. Difference between save() and saveorupdate() in hibernate?**

**Ans:** The important difference between the org.hibernate.Session class methods, save & saveOrUpdate is, save generates a new identifier and results in an INSERT query, whereas saveOrUpdate does an INSERT or an UPDATE. Save method stores an object into the database.

**Q42. What is the difference between save() and persist() in hibernate?**

**Ans:** 

```
Save()
```

1. Returns generated Id after saving. Its return type is `Serializable`;
2. Saves the changes to the database outside of the transaction;
3. Assigns the generated id to the entity you are persisting;
4. `session.save()` for a detached object will create a new row in the table.

```
Persist()
```

1. Does not return generated Id after saving. Its return type is `void`;
2. Does not save the changes to the database outside of the transaction;
3. Assigns the generated Id to the entity you are persisting;
4. `session.persist()` for a detached object will throw a `PersistentObjectException`, as it is not allowed.

**Q43. What are the collection types in Hibernate?**

**Ans.** List, Set, SortedSet, Map, SortedMap, Collection, Bag, 

**Q44. How to implement Joins in Hibernate?** 

**Ans:** Using HQL we can implement joins in hibernate.
HQL Joins – HQL supports inner join, left outer join, right outer join and full join.

**Q45. What is Named SQL Query?**

**Ans:** it might make sense to group all HQL and SQL in one place and use only their reference in the actual data access code. Fortunately, Hibernate allows us to do this with named queries.

A named query is a statically defined query with a predefined unchangeable query string. They're validated when the session factory is created, thus making the application to fail fast in case of an error.

**Q46. What are callback interfaces in hibernate?**

**Ans:** These interfaces are used in the application to receive a notification when some object events occur. Like when an object is loaded, saved or deleted. There is no need to implement callbacks in hibernate applications, but they're useful for implementing certain kinds of generic functionality.

**Q47. What is transaction management in hibernate?**

**Ans:** In a non-managed environment, Hibernate is usually responsible for its own database connection pool. The application developer has to manually set transaction boundaries (begin, commit, or rollback database transactions) themselves.

**Q48. What are the mapping associations used in hibernate?**

**Ans:** One-to-One, One-to-Many, Many-to-One, Many-to-Many

**Q49. What is the is the default transaction factory in hibernate?**

**Ans:** JDBCTransactionFactory is the default transaction factory in hibernate.

**Q50. What is version property in hibernate?**

**Ans:** The <version> property (or @Version annotation) – We know that that Hibernate can provide optimistic locking through a version property on your persistent objects.

**Q51. What does session lock () method do in hibernate?**

**Ans:** The lock() method, with LockOptions.NONE, can be used to associate a detached object to a session and put the object back into a persistence context. 

**Q52. What does evict do in hibernate?**

**Ans:** evict() To detach the object from session cache, hibernate provides evict() method. After detaching the object from the session, any change to object will not be persisted. 

