# Queue

The Queue interface is available in java.util package and extends the Collection interface. The queue collection is used to hold the elements about to be processed and provides various operations like the insertion, removal etc. It is an ordered list of objects with its use limited to insert elements at the end of the list and deleting elements from the start of list i.e. it follows the FIFO or the First-In-First-Out principle

##### **Methods in Queue:**

1. **add()-** This method is used to add elements at the tail of queue. More specifically, at the last of linked-list if it is used, or according to the priority in case of priority queue implementation.
2. **peek()-** This method is used to view the head of queue without removing it. It returns Null if the queue is empty.
3. **element()-** This method is similar to peek(). It throws *NoSuchElementException* when the queue is empty.
4. **remove()-** This method removes and returns the head of the queue. It throws *NoSuchElementException* when the queue is empty.
5. **poll()-** This method removes and returns the head of the queue. It returns null if the queue is empty.
6. **size()-** This method return the no. of elements in the queue.



##### Implementation

1. [PriorityQueue](PriorityQueue.md)
2. [LinkedList](/List/LinkedList.md)
3. [PriorityBlockingQueue](PriorityBlockingQueue.md)
4. [ArrayBlockingQueue](ArrayBlockingQueue.md)
5. [LinkedBlockingQueue](LinkedBlockingQueue.md)
6. [DelayQueue](DelayQueue.md)
7. [TransferQueue](TransferQueue.md)