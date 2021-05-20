# Serialization and Deserialization

Serialization is a mechanism of converting the state of an object into a byte stream. Deserialization is the reverse process where the byte stream is used to recreate the actual Java object in memory. This mechanism is used to persist the object.

The byte stream created is platform independent. So, the object serialized on one platform can be deserialized on a different platform.

To make a Java object serializable we implement the **java.io.Serializable** or **java.io.Externalizable** interface.

**java.io.Serializable** is [marker](../marker_interface/README.md) interface having no fields and methods.

**java.io.Externalizable** provides extra functionality to control over serialization process. We can write few properties of an object. It has two methods 

1. **public** **void** writeExternal(ObjectOutput oo) **throws** IOException
2. **public** **void** readExternal(ObjectInput in) **throws** IOException,  ClassNotFoundException



#### Note - 

```
Constructor calling depends on what interface you implement Serializable or Externalizable while doing deserialization
```



The ObjectOutputStream class contains **writeObject()** method for serializing an Object.

```java
public final void writeObject(Object obj)
                       throws IOException
```

The ObjectInputStream class contains **readObject()** method for deserializing an object.

```java
public final Object readObject() throws IOException, ClassNotFoundException
```



1. If a parent class has implemented Serializable interface then child class doesn’t need to implement it but vice-versa is not true.
2. Only non-static data members are saved via Serialization process.
3. Static data members and transient data members are not saved via Serialization process.So, if you don’t want to save value of a non-static data member then make it transient.
4. Calling of constructor depends on what interface you implement (Serializable or Externalizable)
5. Associated objects must be implementing Serializable or Externalizable interface.



**SerialVersionUID**
The Serialization runtime associates a version number with each Serializable class called a SerialVersionUID, which is used during Deserialization to verify that sender and reciever of a serialized object have loaded classes for that object which are compatible with respect to serialization. If the reciever has loaded a class for the object that has different UID than that of corresponding sender’s class, the Deserialization will result in an **InvalidClassException**. A Serializable class can declare its own UID explicitly by declaring a field name.
It must be static, final and of type long.
i.e- ANY-ACCESS-MODIFIER static final long serialVersionUID=42L;



**Serialver**
The serialver is a tool that comes with JDK. It is used to get serialVersionUID number for Java classes.



**Example of Serializable**

```java
class Demo implements java.io.Serializable { 
    public int a; 
    public String b; 
 
    // Default constructor 
    public Demo(int a, String b) { 
        this.a = a; 
        this.b = b; 
    } 
 
} 
 
class Test { 
    public static void main(String[] args) {
        
        Demo object = new Demo(1, "geeksforgeeks"); 
        String filename = "file.ser"; 
         
        // Serialization  
        try {    
            //Saving of object in a file 
            FileOutputStream file = new FileOutputStream(filename); 
            ObjectOutputStream out = new ObjectOutputStream(file); 
             
            // Method for serialization of object 
            out.writeObject(object); 
             
            out.close(); 
            file.close(); 
             
            System.out.println("Object has been serialized"); 
 
        } catch(IOException ex) { 
            System.out.println("IOException is caught"); 
        } 
 
        Demo object1 = null; 
 
        // Deserialization 
        try {    
            // Reading the object from a file 
            FileInputStream file = new FileInputStream(filename); 
            ObjectInputStream in = new ObjectInputStream(file); 
             
            // Method for deserialization of object 
            object1 = (Demo)in.readObject(); 
             
            in.close(); 
            file.close(); 
             
            System.out.println("Object has been deserialized "); 
            System.out.println("a = "+ object1.a); 
            System.out.println("b = "+ object1.b); 
        } catch (IOException ex) { 
            System.out.println(``"IOException is caught"``); 
        } catch (ClassNotFoundException ex) { 
            System.out.println("ClassNotFoundException is caught"); 
        }  
    } 
} 
```





**Example of Externalizable**

```java
class Employee implements Externalizable  {
    
    private static final long serialVersionUID = 1L;
    private Integer id;
    
    public Employee(){
           System.out.println("No-arg constructor called");
    }
    
    public Employee(Integer id) {
           System.out.println("1-arg constructor called");
           this.id = id;
    }
 
    @Override
    public String toString() {
           return "Employee [id=" + id + "]";
    }
 
    /*
     * define how Serialization process will write objects.  
     */
    @Override
    public void writeExternal(ObjectOutput oo) throws IOException {
           oo.writeInt(id);
    }
    
 
    /*
     * define how deSerialization process will read objects.  
     */
    @Override
    public void readExternal(ObjectInput in) throws IOException,  
    											ClassNotFoundException {
           this.id=in.readInt();
    }
 
}
 
public class ExternalizableConstructorCheck {
 
    public static void main(String[] args) {
 
           Employee object1 = new Employee(8);
 
           try {
               	OutputStream fout = new FileOutputStream("ser.txt");
               	ObjectOutput oout = new ObjectOutputStream(fout);
               	System.out.println("Serialization process has started, serializing employee objects...");
               	oout.writeObject(object1);
               	fout.close();
               	oout.close();
               	System.out.println("Object Serialization completed.");                 
 
               //DeSerialization process >               
                  
               	InputStream fin=new FileInputStream("ser.txt");
               	ObjectInput oin=new ObjectInputStream(fin);
               	System.out.println("\nDeSerialization process has started, displaying employee objects...");
               	Employee emp=(Employee)oin.readObject();
               	System.out.println(emp);
               	fin.close();
         		oin.close();
         		System.out.println("Object DeSerialization completed.");             
                  
           } catch (IOException | ClassNotFoundException  e) {
                  e.printStackTrace();
           }
 
    }
 
}
```

