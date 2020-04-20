# Map

The java.util.Map interface represents a mapping between a key and a value. The Map interface is not a subtype of the [Collection ](https://www.geeksforgeeks.org/collections-in-java-2/)interface. Therefore it behaves a bit different from the rest of the collection types.

A Map cannot contain duplicate keys and each key can map to at most one value.

**Methods in Map Interface:**

1. public Object put(Object key, Object value): This method is used to insert an entry in this map.
2. public void putAll(Map map): This method is used to insert the specified map in this map.
3. public Object remove(Object key): This method is used to delete an entry for the specified key.
4. public Object get(Object key):This method is used to return the value for the specified key.
5. public boolean containsKey(Object key): This method is used to search the specified key from this map.
6. public Set keySet(): This method is used to return the Set view containing all the keys.
7. public Set entrySet(): This method is used to return the Set view containing all the keys and values.

##### Implementation

1. [HashMap](HashMap.md)

2. [LinkedHashMap](LinkedHashMap.md)

3. [TreeMap](TreeMap.md)

4. [EnumMap](EnumMap.md)

5. [WeakHashMap](WeakHashMap.md)

6. [IdentityHashMap](IdentityHashMap.md)

7. [ConcurrentMap](ConcurrentMap.md)

   