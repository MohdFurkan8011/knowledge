# Immutable

Immutable class means that once an object is created, we cannot change its content. In Java, all the [wrapper classes](https://www.geeksforgeeks.org/wrapper-classes-java/) (like Integer, Boolean, Byte, Short) and String class is immutable. We can create our own immutable class as well.

Following are the requirements

1. Declare the class as final so it can’t be extended.

2. Make all fields private so that direct access is not allowed.

3. Don’t provide setter methods for variables

4. Make all **mutable fields final** so that it’s value can be assigned only once.

5. Initialize all the fields via a constructor performing deep copy.

6. Perform cloning of objects in the getter methods to return a copy rather than returning the actual object reference.

   

```java
public final class FinalClassExample {

	private final int id;

	private final String name;

	private final HashMap<String,String> testMap;

	public int getId() {
		return id;
	}
	public String getName() {
		return name;
	}

	/**
 	* Accessor function for mutable objects
 	*/
	public HashMap<String, String> getTestMap() {
		//return testMap;
		return (HashMap<String, String>) testMap.clone();
	}

    /**
     * Constructor performing Deep Copy
     * @param i
     * @param n
     * @param hm
     */

    public FinalClassExample(int i, String n, HashMap<String,String> hm){
        System.out.println("Performing Deep Copy for Object initialization");
        this.id=i;
        this.name=n;
        HashMap<String,String> tempMap=new HashMap<String,String>();
        String key;
        Iterator<String> it = hm.keySet().iterator();
        while(it.hasNext()){
            key=it.next();
            tempMap.put(key, hm.get(key));
        }
        this.testMap=tempMap;
    }
}
```

