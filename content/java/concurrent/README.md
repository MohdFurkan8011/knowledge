# Concurrent Package In Java



Java 5 added a new package to the java platform. the java.util.concurrent package. This package contains a set of classes that makes it easier to develop concurrent applications in java.



1. [BlockingQueue](#blockingqueue)

   ​	a. [ArrayBlockingQueue](#arrayblockingqueue)

   ​	b. [LinkedBlockingQueue](#linkedblockingqueue)

   ​	c. [PriorityBlockingQueue](#priorityblockingqueue)

   ​	d. [DelayQueue](#delayqueue)

   ​	e. [SynchronousQueue](#synchronousqueue)

   ​	f. [BlockingDeque]()

   ​	g. [LinkedBlockingDeque]()

2. [ConcurrentMap]()

3. [CountDownLatch]()

4. [CyclicBarrier]()

5. [Semaphore]()

6. [Exchanger]()

7. [ExecutorService]()

8. [Callable]()

9. [Future]()

10. [Atomic]()

    a. [AtomicBoolean]()

    b. [AtomicInteger]()

    c. [AtomicLong]()

    d. [AtomicReference]()

    e. [AtomicIntegerArray]()

    f. [AtomicLongArray]()

    g. [AtomicReferenceArray]()







#### BlockingQueue

java.util.concurrent.BlockingQueue interface represent a queue which is thread safe to put elements into, and take elements out of from. In other words, multiple threads can be inserting and taking elements concurrently from a Java BlockingQueue without any concurrency issue arising.

For instance, if a thread tries to take an element and there are none left in the queue, the thread can be blocked until there is an element to take. Whether or not the calling thread is blocked depends on what methods you call on the `BlockingQueue`.

##### BlockingQueue Methods

The Java `BlockingQueue` interface has 4 different sets of methods for inserting, removing and examining the elements in the queue. Each set of methods behaves differently in case the requested operation cannot be carried out immediately. Here is a table of the methods:

|             | **Throws Exception** | **Special Value** | **Blocks** | **Times Out**                 |
| ----------- | -------------------- | ----------------- | ---------- | ----------------------------- |
| **Insert**  | `add(o)`             | `offer(o)`        | `put(o)`   | `offer(o, timeout, timeunit)` |
| **Remove**  | `remove(o)`          | `poll()`          | `take()`   | `poll(timeout, timeunit)`     |
| **Examine** | `element()`          | `peek()`          | ` `        | ` `                           |





#### ArrayBlockingQueue

`ArrayBlockingQueue` is a bounded, blocking queue that stores the elements internally in an array. That it is bounded means that it cannot store unlimited amounts of elements. There is an upper bound on the number of elements it can store at the same time. You set the upper bound at instantiation time, and after that it cannot be changed.

The `ArrayBlockingQueue` stores the elements internally in FIFO (First In, First Out) order. The `head` of the queue is the element which has been in queue the longest time, and the `tail` of the queue is the element which has been in the queue the shortest time.

```java
BlockingQueue<String> queue = new ArrayBlockingQueue<String>(1024);
queue.put("1");
String string = queue.take();
```





#### LinkedBlockingQueue

The `LinkedBlockingQueue` keeps the elements internally in a linked structure (linked nodes). This linked structure can optionally have an upper bound if desired. If no upper bound is specified, `Integer.MAX_VALUE` is used as the upper bound.

```java
BlockingQueue<String> unbounded = new LinkedBlockingQueue<String>();
BlockingQueue<String> bounded   = new LinkedBlockingQueue<String>(1024);

bounded.put("Value");

String value = bounded.take();
```





#### PriorityBlockingQueue

The `PriorityBlockingQueue` is an unbounded concurrent queue. It uses the same ordering rules as the `java.util.PriorityQueue` class. You cannot insert null into this queue.

All elements inserted into the `PriorityBlockingQueue` must implement the `java.lang.Comparable` interface. The elements thus order themselves according to whatever priority you decide in your `Comparable` implementation.

```java
BlockingQueue queue   = new PriorityBlockingQueue();

//String implements java.lang.Comparable
queue.put("Value");

String value = queue.take();
```





#### DelayQueue

The `DelayQueue` blocks the elements internally until a certain delay has expired. The elements must implement the interface `java.util.concurrent.Delayed`. Here is how the interface looks:

```java
public interface Delayed extends Comparable<Delayed< {

 public long getDelay(TimeUnit timeUnit);

}
```

The value returned by the `getDelay()` method should be the delay remaining before this element can be released. If 0 or a negative value is returned, the delay will be considered expired, and the element released at the next `take()` etc. call on the `DelayQueue`.

The `TimeUnit` instance passed to the `getDelay()` method is an `Enum` that tells which time unit the delay should be returned in. The `TimeUnit` enum can take these values:

```java
public class DelayQueueExample {

    public static void main(String[] args) {
        DelayQueue queue = new DelayQueue();

        Delayed element1 = new DelayedElement();

        queue.put(element1);

        Delayed element2 = queue.take();
    }
}
```





#### SynchronousQueue

The *SynchronousQueue* only has **two supported operations: \*take()\* and \*put(),\* and both of them are blocking**.

For example, when we want to add an element to the queue, we need to call the *put()* method. That method will block until some other thread calls the *take()* method, signaling that it is ready to take an element.





#### BlockingDeque

The `BlockingDeque` class is a `Deque` which blocks threads tring to insert or remove elements from the deque, in case it is either not possible to insert or remove elements from the deque.

A `deque` is short for "Double Ended Queue". Thus, a `deque` is a queue which you can insert and take elements from, from both ends.

##### BlockingDeque methods

A `BlockingDeque` has 4 different sets of methods for inserting, removing and examining the elements in the deque. Each set of methods behaves differently in case the requested operation cannot be carried out immediately. Here is a table of the methods:

|             | **Throws Exception** | **Special Value** | **Blocks**     | **Times Out**                      |
| ----------- | -------------------- | ----------------- | -------------- | ---------------------------------- |
| **Insert**  | `addFirst(o)`        | `offerFirst(o)`   | `putFirst(o)`  | `offerFirst(o, timeout, timeunit)` |
| **Remove**  | `removeFirst(o)`     | `pollFirst(o)`    | `takeFirst(o)` | `pollFirst(timeout, timeunit)`     |
| **Examine** | `getFirst(o)`        | `peekFirst(o)`    | ` `            | ` `                                |

|             | **Throws Exception** | **Special Value** | **Blocks**    | **Times Out**                     |
| ----------- | -------------------- | ----------------- | ------------- | --------------------------------- |
| **Insert**  | `addLast(o)`         | `offerLast(o)`    | `putLast(o)`  | `offerLast(o, timeout, timeunit)` |
| **Remove**  | `removeLast(o)`      | `pollLast(o)`     | `takeLast(o)` | `pollLast(timeout, timeunit)`     |
| **Examine** | `getLast(o)`         | `peekLast(o)`     | ` `           | ` `                               |





#### LinkedBlockingDeque

The `LinkedBlockingDeque` class implements the `BlockingDeque` interface. 

The word `Deque` comes from the term "Double Ended Queue". A `Deque` is thus a queue where you can insert and remove elements from both ends of the queue.

The `LinkedBlockingDeque` is a `Deque` which will block if a thread attempts to take elements out of it while it is empty, regardless of what end the thread is attempting to take elements from.

Here is how to instantiate and use a `LinkedBlockingDeque`:

```java
BlockingDeque<String> deque = new LinkedBlockingDeque<String>();

deque.addFirst("1");
deque.addLast("2");

String two = deque.takeLast();
String one = deque.takeFirst();
```

