# Cloneable

Cloneable interface is present in java.lang package. There is a method clone() in [Object](https://www.geeksforgeeks.org/object-class-in-java/) class. A class that implements the Cloneable interface indicates that it is legal for clone() method to make a field-for-field copy of instances of that class.
Invoking Object’s clone method on an instance of the class that does not implement the Cloneable interface results in an exception CloneNotSupportedException being thrown. By convention, classes that implement this interface should override Object.clone() method.

```java
class A implements Cloneable { 
    int i; 
    String s; 
  
    // A class constructor 
    public A(int i,String s) { 
        this.i = i; 
        this.s = s; 
    } 
  
    // Overriding clone() method 
    // by simply calling Object class 
    // clone() method. 
    @Override
    protected Object clone() throws CloneNotSupportedException { 
        return super.clone(); 
    } 
    
}
```



##### **Deep Copy vs Shallow Copy**

##### Shallow copy

- **Shallow copy** is method of copying an object and is followed by default in cloning. In this method the fields of an old object X are copied to the new object Y. While copying the object type field the reference is copied to Y i.e object Y will point to same location as pointed out by X. If the field value is a primitive type it copies the value of the primitive type.
- Therefore, any changes made in referenced objects in object X or Y will be reflected in other object.

*Shallow copies are cheap and simple to make. In above example, we created a shallow copy of object.*

##### Deep copy

- If we want to create a deep copy of object X and place it in a new object Y then new copy of any referenced objects fields are created and these references are placed in object Y. This means any changes made in referenced object fields in object X or Y will be reflected only in that object and not in the other. In below example, we create a deep copy of object.
- A deep copy copies all fields, and makes copies of dynamically allocated memory pointed to by the fields. A deep copy occurs when an object is copied along with the objects to which it refers.



##### Deep copy example

```java
class Course implements Cloneable {
    
    String subject1; 
    String subject2; 
    String subject3;
    
    public Course(String sub1, String sub2, String sub3) {
        this.subject1 = sub1; 
        this.subject2 = sub2; 
        this.subject3 = sub3;
    }
    
    protected Object clone() throws CloneNotSupportedException {
        return super.clone();
    }
}
```

```java
class Student implements Cloneable {
    
    int id; 
    String name; 
    Course course;
 
    public Student(int id, String name, Course course) {
        this.id = id; 
        this.name = name; 
        this.course = course;
    }
    //Overriding clone() method to create a deep copy of an object. 
    protected Object clone() throws CloneNotSupportedException {
        Student student = (Student) super.clone(); 
        student.course = (Course) course.clone(); 
        return student;
    }
    
}
```

