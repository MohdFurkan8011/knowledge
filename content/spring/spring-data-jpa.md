# Spring Data JPA



- [Interview QA](#interview-qa) 

  

#### Interview QA

**Q1. What is Spring Data JPA?**

**Ans:** Spring Data JPA is one of Spring Data module which provides predefined repository methods to perform CRUD operation. Using Spring Data JPA we define the repository interface and query methods(query creation from method names) to access the data from the database.

**Q2. How to create a custom repository in Spring Data JPA?**

**Ans:** We can create custom repository extending any of these interfaces according to need.

- **Repository**

  Top-level interface defined in Spring Data Hierarchy. This is a marker interface i.e doesn’t contain any method.

- **CrudRepository**

  The CrudRepository interface extends Repository interface, provides methods to perform CRUD operation.

- **PagingAndSortingRepository**

  The PagingAndSortingRepository interface extends CrudRepository interface and provides additional methods to retrieve entities using the pagination and sorting.

- **JpaRepository**

  The JpaRepository interface extends PagingAndSortingRepository and QueryByExampleExecutor interface, provides some additional batch methods.

  flush(), saveAndFlush(), deleteInBatch() 

- **QueryByExampleExecutor**

  The QueryByExampleExecutor interface used to execute Query by Example.

- **SimpleJpaRepository**

  The SimpleJpaRepository is the implementation class of the CrudRepository interface.

  

**Q3. How you will write custom method in the repository in Spring Data JPA? What are rules to define Query methods(query creation from method names)?**

**Ans:** 

**Rule 1** – The name of the query method must start with findBy or getBy or queryBy or countBy or readBy prefix. The findBy is mostly used by the developer.

For example findByName(String name), getByName(String name), queryByName(String name), countByName(String name), readByName(String name)

**Rule 2** – The first character of field name should capital letter. Although if we write the first character of the field in small then it will work but we should use camelcase for the method name.

**Rule 3** – While using findBy or getBy or queryBy or countBy or readBy the character B must be in capital letter, else we will get an exception while deployment.

**Rule 4** – We can write the query method using multiple fields using predefined keywords(eg. And, Or etc.) but these keywords are case sensitive. We must use “And” instead of “and”.

**Write query method using @Query.**

```java
@Query("select s from Student s where s.name = ?1")
List<Student> getStudents(String name);
```

**Writing the Named Parameter @Query.**

```java
@Query("select s from Student s where s.name = :name")
List<Student> findByName(@Param("name") String name);
```

**Q4. What are the features/benefits of Spring Data JPA?**

**Ans:** 

- Spring Data JPA provides features to Query creation from method names. For example, consider we have a method defined in Studentrepository `public List<Student> findByName(String name);`

- We can write complex query using @Query annotation in Spring Data JPA.

  ```java
  @Query("select s from Student s where s.name = ?1")
  List<Student> getStudents(String name);
  ```

- @NamedQuery And @NamedQueries

  ```java
  @NamedQuery(name = "Student.findByName", query = "select s from Student s where s.name = ?1")
  
  @NamedQueries({ @NamedQuery(name = "Student.findByName1", query = "select s from Student s where s.name = ?1"),
  		@NamedQuery(name = "Student.findByNameAndRollNumber", query = "select s from Student s where s.name = ?1 and s.rollNumber = ?2"),
  		@NamedQuery(name = "Student.findByNameOrRollNumber", query = "select s from Student s where s.name = ?1 or s.rollNumber = ?2") })
  ```

- @NamedNativeQuery

  ```java
  @NamedNativeQuery(name = "Student.findByName", query = "select * from Student where name = ?1", resultClass = Student.class)
  ```

  

**Q5. How to enable Spring Data JPA features.**

**Ans:** @EnableJpaRepositories(basePackages = "")

**Q6. How CrudRepository save() methods internally works in Spring Data JPA?**

**Ans:** The CrudRepository’s save() method is used to perform save as well as update operation both.

If we try to save entity first time then persist() method will get invoked and if we try to update the same entity merge() will get invoked.

```java
public S save(S entity) {
 
		if (entityInformation.isNew(entity)) {
		em.persist(entity);
		return entity;
		} else {
		return em.merge(entity);
		}
	}
```

**Q7. Tell something about the CrudRepository saveAll() method.**

**Ans:** The CrudRepository saveAll() method used to save multiple entities and internally annotated with @Transactional annotation. It internally uses save() method only as below.

**Q8. How to write a query method for sorting using Spring Data JPA? **

**Ans:** studentRepository.findByUniversityOrderByNameAsc(university);

**Q9. How to implement projection using Spring Data JPA? **

**Ans:** 

- By interface (open and close interface)
- By class

**Q10. Difference between findById() and getOne() in Spring Data JPA?**

**Ans:** 

| findById()                                                   | getOne()                                                     |
| :----------------------------------------------------------- | ------------------------------------------------------------ |
| The findById() method is available in CrudRepository interface. | The getOne() method is available in JpaRepositpry interface. |
| The findById() method will return null if the record doesn’t exist in the database. | The getOne() method throw EntityNotFoundException if the record doesn’t exist in the database. |
| Internally findById() method use EntityManger find() method. | Internally getOne() method use EntityManger getReference() method. |
| Calling `findById()` returns a eager fetched entity.         | Calling `getOne()` returns a lazily fetched entity.          |

**Q11. Difference between delete() vs deleteInBatch() Methods in Spring Data JPA. **

| delete()                                                     | deleteInBatch()                                              |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| The delete() method has been defined in the CrudRepository interface | The deleteInBatch() has been defined in the JpaRepository interface |
| The delete() method internally uses EntityManager’s remove() method | deleteInBatch() prepares the query and collect some other information and directly calls the executeUpdate() method. |
| delete() method, we can delete a single record at a time     | whereas using deleteInBatch() we can delete multiple records. |
| The delete() method is a little slower                       | deleteInBatch() is faster than delete()                      |

**Q12. Difference between deleteAll() Vs deleteAllInBatch() in Spring Data JPA.**

**Ans:**

- void deleteAll(Iterable<? extends T> entities) - delete all passed records.

- deleteAll()

- ```java
  public void deleteAll() {
  
  		for (T element : findAll()) {
  			delete(element);
  		}
  	}
  ```

- void deleteAllInBatch() - Using deleteAllInBatch() method we can delete all entities from database. No need to pass entities as parameters.

**Q13. How to write named parameters in Spring Data JPA?**

**Ans:** @Param and @Query annotations used to define Named Parameters.

```java
@Query("select s from Student s where s.name = :name")
List<Student> findByName(@Param("name") String name);
```

**Q14. What will happen when we define wrong Query Methods in Spring Data JPA?**

**Ans:** while deployment we will get an error.

**Q15. How to define case insensitive search Query Methods in Spring Data JPA?**

**Ans:** 

```java
public List<Student> findByNameIgnoreCase(String name);
```

**Q16. List of important keywords and corresponding Query Methods. **

| Keyword            | Query methods                   | JPQL                                                         |
| :----------------- | :------------------------------ | :----------------------------------------------------------- |
| And                | findByLastnameAndFirstname      | ...where x.lastname = ?1 and x.firstname = ?2                |
| Or                 | findByLastnameOrFirstname       | ...where x.lastname = ?1 or x.firstname = ?2                 |
| Is, Equals         | findByFirstnameEquals           | ...where x.firstname = ?1                                    |
| Between            | findByStartDateBetween          | ...where x.startDate between ?1 and ?                        |
| LessThan           | findByAgeLessThan               | ...where x.age < ?1                                          |
| LessThanEqual      | findByAgeLessThanEqual          | ...where x.age <= ?1< td>                                    |
| GreaterThan        | findByAgeGreaterThan            | ...where x.age > ?1                                          |
| GreaterThanEqual   | findByAgeGreaterThanEqual       | ...where x.age >= ?1                                         |
| After              | findByStartDateAfter            | ...where x.startDate > ?1                                    |
| Before             | findByStartDateBefore           | ...where x.startDate < ?1                                    |
| IsNull             | findByAgeIsNull                 | ...where x.age is null                                       |
| IsNotNull, NotNull | findByAge(Is)NotNull            | ...where x.age not null                                      |
| Like               | findByFirstnameLike             | ...where x.firstname like ?1                                 |
| NotLike            | findByFirstnameNotLike          | ...where x.firstname not like ?1                             |
| StartingWith       | findByFirstnameStartingWith     | ...where x.firstname like ?1 (parameter bound with appended %) |
| EndingWith         | findByFirstnameEndingWith       | ...where x.firstname like ?1 (parameter bound with prepended %) |
| Containing         | findByFirstnameContaining       | ...where x.firstname like ?1 (parameter bound wrapped in %)  |
| OrderBy            | findByAgeOrderByLastnameDesc    | ...where x.age = ?1 order by x.lastname desc                 |
| Not                | findByLastnameNot               | ...where x.lastname <> ?1                                    |
| In                 | findByAgeIn(Collection ages)    | ...where x.age in ?1                                         |
| NotIn              | findByAgeNotIn(Collection ages) | ...where x.age not in ?1                                     |
| True               | findByActiveTrue()              | ...where x.active = true                                     |
| False              | findByActiveFalse()             | ...where x.active = false                                    |
| IgnoreCase         | findByFirstnameIgnoreCase       | ...where UPPER(x.firstame) = UPPER(?1)                       |



**Q17. What does the @Id annotation do?**

**Ans:** The **@Id** annotation marks a field as the primary key for that particular table. This is a unique identifier for each entry in the table. This annotation is typically used with **@GeneratedValue** to automatically generate an unique id for each entry in the table.

**Q18. What does the @Entity annotation do?**

**Ans:** The **@Entity** annotation indicates a class represents a relational table in the database.

**Q19. What is the difference between FetchType.Eager and FetchType.Lazy?**

**Ans:** FetchType attribute indicates how whether records will be eagerly or lazily loaded from the database.

**Q20. Is the CrudRepository interface part of JPA?**

**Ans:** No. CrudRepository is an interface exposed by Spring Data framework for more easily interacting with JPA implementations like Hibernate

**Q21. Is Spring Data JPA an implementation of the JPA specification?**

**Ans:** No. Spring Data simply makes it easier to interface with a JPA specification like Hibernate

**Q22. Is the @Column annotation required for mapping fields to columns?**

**Ans:** No. The @Column field allows you to optionally override the name of the column that the entity class field maps to in the database table. It is not required.

**Q23. In a @OneToMany relationship, what does the "mappedBy" attribute indicate?**

**Ans:** mappedBy is an attribute that specifies the owning side of a one to many relationship. For example, if you want to establish a one to many relationship between authors and books you would specify **mappedBy="authors"** on the Books entity.

**Q24. What does the @EnableJpaRepositories annotation do?**

**Ans:** This annotation enables the automatic generation of JPA repositories. Any class which implements CrudRepository interface will generate a repository when this annotation is present.