# IdentityHashMap

IdentityHashMap implements Map, Serializable and Clonable interfaces and extends AbstractMap class.
This class is not a general-purpose Map implementation. While this class implements the [Map](https://www.geeksforgeeks.org/map-interface-java-examples/) interface, it intentionally violates Map’s general contract, which mandates the use of the equals method when comparing objects.

This class is used when the user requires the objects to be compared via reference.



**IdentityHashMap vs HashMap**

- IdentityHashMap uses equality operator “==” for comparing keys and values while HashMap uses equals method for comparing keys and values inside Map.
- Since IdentityHashMap doesn’t use equals() its comparatively faster than HashMap for object with expensive equals().
- IdentityHashMap doesn’t require keys to be immutable as it is not relied on equals().

