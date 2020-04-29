# Exception Handling

**Dictionary Meaning:** Exception is an abnormal condition.

In Java, an exception is an event that disrupts the normal flow of the program. It is an **object** which is thrown at runtime.



![](D:\knowledge\content\java\exception\Exception.PNG)





#### Types of exceptions

1. **Checked exception**

   The classes which directly inherit Throwable class **except RuntimeException and Error** are known as checked exceptions e.g. **IOException, SQLException** etc. Checked exceptions are checked at compile-time.

2. **Unchecked exception**

   The classes which inherit **RuntimeException** are known as unchecked exceptions e.g. **ArithmeticException, NullPointerException, ArrayIndexOutOfBoundsException** etc. Unchecked exceptions are not checked at compile-time, but they are checked at runtime

3. **Error**

   Error is irrecoverable e.g. OutOfMemoryError, VirtualMachineError, AssertionError etc.

   

**Keywords**

1. **try**

   The "try" keyword is used to specify a block where we should place exception code. The try block must be followed by either catch or finally. It means, we can't use try block alone.

2. **catch**

   The "catch" block is used to handle the exception. It must be preceded by try block which means we can't use catch block alone. It can be followed by finally block later.

3. **finally**

   The "finally" block is used to execute the important code of the program. It is executed whether an exception is handled or not.

4. **throw**

   The "throw" keyword is used to throw an exception.

5. **throws**

   The "throws" keyword is used to declare exceptions. It doesn't throw an exception. It specifies that there may occur an exception in the method. It is always used with method signature.



#### **ExceptionHandling with MethodOverriding in Java**

There are many rules if we talk about methodoverriding with exception handling. The Rules are as follows:

- If the superclass method does not declare an exception
  - If the superclass method does not declare an exception, subclass overridden method cannot declare the checked exception but it can declare unchecked exception.
- If the superclass method declares an exception
  - If the superclass method declares an exception, subclass overridden method can declare same, subclass exception or no exception but cannot declare parent exception.



**Notes**

1. **Exception  Propagation**

   An exception is first thrown from the top of the stack and if it is not caught, it drops down the call stack to the previous method,If not caught there, the exception again drops down to the previous method, and so on until they are caught or until they reach the very bottom of the call stack. This is called exception propagation.

   **By default Unchecked Exceptions are forwarded in calling chain (propagated).**

   with the help of throws keyword you can get exception propagation with checked exception.

   

2. Try with resource(java 1.5 features to close resources automatically). It happen just because of Autoclosable interface, our resource should implement this interface.

   **From java 1.7  it is possible to have only try block,  possible by try with resource.**

3. **ClassNotFoundException** when you load a class with does not exists in classpath,
   **NoClassDefFoundError** class is available at compile time, but not available at run time.

4. Multiple catch rule, (In last catch, parent exception should be) 

5. Nested try (try into another try)

6. Rethrow an exception

7. **Custom exception**

8. Union catch blocks

   ```java
    try (Scanner contents = new Scanner(new File(playerFile))) {
       return Integer parseInt(contents.nextLine());
     } catch(IOException | NumberFormatException e) {
       logger.warn("Failed to load score!", e);
       return 0;
     }
   ```


