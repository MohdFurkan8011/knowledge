# Concurrent Package In Java



Java 5 added a new package to the java platform. the java.util.concurrent package. This package contains a set of classes that makes it easier to develop concurrent applications in java.



1. [BlockingQueue](#blockingqueue)

   ​	a. [ArrayBlockingQueue](#arrayblockingqueue)

   ​	b. [LinkedBlockingQueue](#linkedblockingqueue)

   ​	c. [PriorityBlockingQueue](#priorityblockingqueue)

   ​	d. [DelayQueue](#delayqueue)

   ​	e. [SynchronousQueue](#synchronousqueue)

   ​	f. [BlockingDeque](#blockingdeque)

   ​	g. [LinkedBlockingDeque](#linkedblockingdeque)

2. [ConcurrentMap](#concurrentmap)

3. [CountDownLatch](#countdownlatch)

4. [CyclicBarrier](#cyclicbarrier)

5. [Semaphore](#semaphore)

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

The `BlockingDeque` class is a `Deque` which blocks threads trying to insert or remove elements from the deque, in case it is either not possible to insert or remove elements from the deque.

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





#### ConcurrentMap

The `java.util.concurrent.ConcurrentMap` interface represents a Map which is capable of handling concurrent access (puts and gets) to it.

The `ConcurrentMap` has a few extra atomic methods in addition to the methods it inherits from its superinterface, `java.util.Map`.

##### ConcurrentHashMap

The `ConcurrentHashMap` is very similar to the `java.util.HashTable` class, except that `ConcurrentHashMap` offers better concurrency than `HashTable` does. `ConcurrentHashMap` does not lock the `Map` while you are reading from it. Additionally, `ConcurrentHashMap` does not lock the entire `Map` when writing to it. It only locks the part of the `Map` that is being written to, internally.

Another difference is that `ConcurrentHashMap` does not throw `ConcurrentModificationException` if the `ConcurrentHashMap` is changed while being iterated.



#### CountDownLatch

A `java.util.concurrent.CountDownLatch` is a concurrency construct that allows one or more threads to wait for a given set of operations to complete.

A `CountDownLatch` is initialized with a given count. This count is decremented by calls to the `countDown()` method. Threads waiting for this count to reach zero can call one of the `await()` methods. Calling `await()` blocks the thread until the count reaches zero.

Below is a simple example. After the `Decrementer` has called `countDown()` 3 times on the `CountDownLatch`, the waiting `Waiter` is released from the `await()` call.

```java
CountDownLatch latch = new CountDownLatch(3);

Waiter      waiter      = new Waiter(latch);
Decrementer decrementer = new Decrementer(latch);

new Thread(waiter)     .start();
new Thread(decrementer).start();

Thread.sleep(4000);
```

```java
public class Waiter implements Runnable{

    CountDownLatch latch = null;

    public Waiter(CountDownLatch latch) {
        this.latch = latch;
    }

    public void run() {
        try {
            latch.await();
        } catch (InterruptedException e) {
            e.printStackTrace();
        }

        System.out.println("Waiter Released");
    }
}
```

```java
public class Decrementer implements Runnable {

    CountDownLatch latch = null;

    public Decrementer(CountDownLatch latch) {
        this.latch = latch;
    }

    public void run() {

        try {
            Thread.sleep(1000);
            this.latch.countDown();

            Thread.sleep(1000);
            this.latch.countDown();

            Thread.sleep(1000);
            this.latch.countDown();
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
    }
}
```





#### CyclicBarrier

The `java.util.concurrent.CyclicBarrier` class is a synchronization mechanism that can synchronize threads progressing through some algorithm. In other words, it is a barrier that all threads must wait at, until all threads reach it, before any of the threads can continue. Here is a diagram illustrating that.

The threads wait for each other by calling the `await()` method on the `CyclicBarrier`. Once N threads are waiting at the `CyclicBarrier`, all threads are released and can continue running.

`CyclicBarriers are used in programs in which we have a fixed number of threads that must wait for each other to reach a common point before continuing execution.`

The barrier is called cyclic because it can be re-used after the waiting threads are released.

The constructor for a *CyclicBarrier* is simple. It takes a single integer that denotes the number of threads that need to call the *await()* method on the barrier instance to signify reaching the common execution point:



#### Semaphore

The `java.util.concurrent.Semaphore` class is a counting semaphore. That means that it has two main methods:

- acquire()
- release()

The counting semaphore is initialized with a given number of "permits". For each call to `acquire()` a permit is taken by the calling thread. For each call to `release()` a permit is returned to the semaphore. Thus, at most N threads can pass the `acquire()` method without any `release()` calls, where N is the number of permits the semaphore was initialized with. The permits are just a simple counter.

If you use a semaphore to send signals between threads, then you would typically have one thread call the `acquire()` method, and the other thread to call the `release()` method.

If no permits are available, the `acquire()` call will block until a permit is released by another thread. Similarly, a `release()` calls is blocked if no more permits can be released into this semaphore.

##### Fairness

No guarantees are made about [fairness](http://tutorials.jenkov.com/java-concurrency/starvation-and-fairness.html) of the threads acquiring permits from the `Semaphore`. That is, there is no guarantee that the first thread to call `acquire()` is also the first thread to obtain a permit. If the first thread is blocked waiting for a permit, then a second thread checking for a permit just as a permit is released, may actually obtain the permit ahead of thread 1.

If you want to enforce fairness, the `Semaphore` class has a constructor that takes a boolean telling if the semaphore should enforce fairness. Enforcing fairness comes at a performance / concurrency penalty, so don't enable it unless you need it.

```java
Semaphore semaphore = new Semaphore(1, true);
```





#### Exchanger

The `java.util.concurrent.Exchanger` class represents a kind of rendezvous point where two threads can exchange objects. Here is an illustration of this mechanism.

```java
Exchanger exchanger = new Exchanger();

ExchangerRunnable exchangerRunnable1 =
        new ExchangerRunnable(exchanger, "A");

ExchangerRunnable exchangerRunnable2 =
        new ExchangerRunnable(exchanger, "B");

new Thread(exchangerRunnable1).start();
new Thread(exchangerRunnable2).start();
```

```java
public class ExchangerRunnable implements Runnable{

    Exchanger exchanger = null;
    Object    object    = null;

    public ExchangerRunnable(Exchanger exchanger, Object object) {
        this.exchanger = exchanger;
        this.object = object;
    }

    public void run() {
        try {
            Object previous = this.object;

            this.object = this.exchanger.exchange(this.object);

            System.out.println(
                    Thread.currentThread().getName() +
                    " exchanged " + previous + " for " + this.object
            );
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
    }
}
```

