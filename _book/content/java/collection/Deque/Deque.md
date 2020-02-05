# Deque

The java.util.Deque interface is a subtype of the [java.util.Queue](https://www.geeksforgeeks.org/queue-interface-java/) interface. The Deque is related to the double-ended queue that supports addition or removal of elements from either end of the data structure, it can be used as a [queue (first-in-first-out/FIFO)](https://www.geeksforgeeks.org/queue/) or as a [stack (last-in-first-out/LIFO)](https://www.geeksforgeeks.org/stack/). These are faster than Stack and LinkedList.

**Methods of Deque:**

1. **add(element):** Adds an element to the tail.
2. **addFirst(element):** Adds an element to the head.
3. **addLast(element):** Adds an element to the tail.
4. **offer(element):** Adds an element to the tail and returns a boolean to explain if the insertion was successful.
5. **offerFirst(element):** Adds an element to the head and returns a boolean to explain if the insertion was successful.
6. **offerLast(element):** Adds an element to the tail and returns a boolean to explain if the insertion was successful.
7. **iterator():** Returna an iterator for this deque.
8. **descendingIterator():** Returns an iterator that has the reverse order for this deque.
9. **push(element):** Adds an element to the head.
10. **pop(element):** Removes an element from the head and returns it.
11. **removeFirst():** Removes the element at the head.
12. **removeLast():** Removes the element at the tail.
13. **poll():** Retrieves and removes the head of the queue represented by this deque (in other words, the first element of this deque), or returns null if this deque is empty.
14. **pollFirst():** Retrieves and removes the first element of this deque, or returns null if this deque is empty.
15. **pollLast():** Retrieves and removes the last element of this deque, or returns null if this deque is empty.
16. **peek():** Retrieves, but does not remove, the head of the queue represented by this deque (in other words, the first element of this deque), or returns null if this deque is empty.
17. **peekFirst():** Retrieves, but does not remove, the first element of this deque, or returns null if this deque is empty.
18. **peekLast():** Retrieves, but does not remove, the last element of this deque, or returns null if this deque is empty.

##### Implementation

1. [LinkedList](../List/LinkedList.md)
2. [ArrayDeque](ArrayDeque.md)
3. [LinkedBlockingDeque](LinkedBlockingDeque.md)