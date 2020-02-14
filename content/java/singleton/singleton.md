

# Singleton Class

The singleton pattern is one of the simplest design patterns. Sometimes we need to have only one instance of our class for example a single DB connection shared by multiple objects as creating a separate DB connection for every object may be costly. Similarly, there can be a single configuration manager or error manager in an application that handles all problems instead of creating multiple managers.

1. [Method 1](#method-1)
2. [Method 2](#method-2)
3. [Method 3](#method-3)
4. [Method 4](#method-4)

[When Singleton design pattern breaks](#when-singleton-design-pattern-breaks)



###### Method 1

```java
// Classical Java implementation of singleton  
// design pattern 
class Singleton { 
    private static Singleton obj; 
 
    // private constructor to force use of 
    // getInstance() to create Singleton object 
    private Singleton() {} 
 
    public static Singleton getInstance() { 
        if (obj == null) 
            obj = new Singleton(); 
        return obj; 
    } 
}
```

###### Problem with method 1

The main problem with above method is that it is not thread safe.



###### Method 2

```java
// Thread Synchronized Java implementation of  
// singleton design pattern 
class Singleton {     
    private static Singleton obj; 
 
    private Singleton() {} 
 
    // Only one thread can execute this at a time 
    public static synchronized Singleton getInstance() { 
        if (obj == null) 
            obj = new Singleton(); 
        return obj; 
    } 
} 
```

###### Problem with method 2

The main disadvantage of this is method is that using synchronized every time while creating the singleton object is expensive and may decrease the performance of your program. However if performance of getInstance() is not critical for your application this method provides a clean and simple solution.



###### Method 3

```java
// Static initializer based Java implementation of 
// singleton design pattern 
class Singleton { 
    private static Singleton obj = new Singleton(); 
 
    private Singleton() {} 
 
    public static Singleton getInstance() { 
        return obj; 
    } 
} 
```



###### Method 4

Double checked Locking

```java
// Double Checked Locking based Java implementation of 
// singleton design pattern 
class Singleton { 
    private volatile static Singleton obj; 
 
    private Singleton() {} 
 
    public static Singleton getInstance() { 
        if (obj == null) { 
            // To make thread safe 
            synchronized (Singleton.class) { 
                // check again as multiple threads 
                // can reach above step 
                if (obj == null) 
                    obj = new Singleton(); 
            } 
        } 
        return obj; 
    } 
}
```





#### When Singleton design pattern breaks

1. [Reflection](#reflection)
2. [Deserialization](#deserialization)
3. [Clone](#clone)



###### Reflection

Java Reflection is an API used to examine or modify the behavior of methods, classes, and interfaces at runtime. Using the Reflection API, we can create multiple objects in the `Singleton` class. Consider the following example

```java
public class ReflectionSingleton {
    
    public static void main(String[] args)  {
        Singleton objOne = Singleton.getInstance();
        Singleton objTwo = null;
        try {
            Constructor constructor = Singleton.class.getDeclaredConstructor();
            constructor.setAccessible(true);
            objTwo = (Singleton) constructor.newInstance();
        } catch (Exception ex) {
            System.out.println(ex);
        }
        System.out.println("Hashcode of Object 1 - "+objOne.hashCode());
        System.out.println("Hashcode of Object 2 - "+objTwo.hashCode());
    }
    
}
```

###### Ans. 

Throws exception from constructor if instance already created.



###### Deserialization

```java
public class DeserializationSingleton {
    
    public static void main(String[] args) throws Exception {
        Singleton instanceOne = Singleton.getInstance();
        ObjectOutput out = new ObjectOutputStream(new FileOutputStream("file.text"));
        out.writeObject(instanceOne);
        out.close();
        ObjectInput in = new ObjectInputStream(new FileInputStream("file.text"));
        Singleton instanceTwo = (Singleton) in.readObject();
        in.close();
        System.out.println("hashCode of instance 1 is - " + instanceOne.hashCode());
        System.out.println("hashCode of instance 2 is - " + instanceTwo.hashCode());
    }
    
}
```

###### Ans.

```java
protected Object readResolve() { 
	return instance; 
}
```



###### Clone

###### Ans.

```java
@Override
protected Object clone() throws CloneNotSupportedException  {
	throw new CloneNotSupportedException();
}
```

