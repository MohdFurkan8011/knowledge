# Clone

Cloning is a process of creating a replica or copy of [java]() object, clone method Java.lang.Object is used to create copy or replica of an object. java objects which implement Cloneable interface are eligible for using the clone method.

###### Shallow Copy

The default implementation of the clone method creates a shallow copy of the source object, it means a new instance of type Object is created, it copies all the fields to a new instance and returns a new object of type ‘Object’. This Object explicitly needs to be typecast in object type of source object.

This object will have an exact copy of all the fields of source object including the primitive type and object references. If the source object contains any references to other objects in field then in the new instance will have only references to those objects, a copy of those objects is not created. This means if we make changes in shallow copy then changes will get reflected in the source object. Both instances are not independent.



```java
class Department {
    
    String empId;
	String grade; 
	String designation;
 
	public Department(String empId, String grade, String designation) {
    	this.empId = empId; 
    	this.grade = grade; 
    	this.designation = designation;
	}
    
}

class Employee implements Cloneable {
    
    int id; 
    String name; 
    Department dept;
 
    public Employee(int id, String name, Department dept) {
        this.id = id; 
        this.name = name; 
        this.dept = dept;
    } 
    // Default version of clone() method. It creates shallow copy of an object. 
    protected Object clone() throws CloneNotSupportedException {
        return super.clone();
    }
}
```


###### **Deep Copy**

The deep copy of an object will have an exact copy of all the fields of source object like a shallow copy, but unlike sallow copy if the source object has any reference to object as fields, then a replica of the object is created by calling clone method. This means that both source and destination objects are independent of each other. Any change made in the cloned object will not impact the source object.



```java
class Department implements Cloneable {
    
    String empId;
	String grade; 
	String designation;
    
	public Department(String empId, String grade, String designation) {
    	this.empId = empId; 
    	this.grade = grade; 
    	this.designation = designation;
	}
	//Default version of clone() method.
	protected Object clone() throws CloneNotSupportedException {
    	return super.clone();
	}
    
}

class Employee implements Cloneable {
    
    int id; 
    String name; 
    Department dept;
 
    public Employee(int id, String name, Department dept) {
        this.id = id; 
        this.name = name; 
        this.dept = dept;
    } 
    // Overriding clone() method to create a deep copy of an object. 
    protected Object clone() throws CloneNotSupportedException {
        Employee emp = (Employee) super.clone(); 
        emp.dept = (Department) dept.clone(); 
        return emp;
    }
    
}
```
