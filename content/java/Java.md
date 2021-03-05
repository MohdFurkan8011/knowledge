# Java

 

- [Introduction](#introduction)
- [Types of applications](#types-of-applications)
- [Java Plateforms Editions](#java-platforms-editions)
- [Features of Java](#features-of-java)
- [C++ vs Java](#c++-vs-java)
- [Difference between JDK JRE and JVM](#difference-between-jdk-jre-and-jvm)

#### Introduction

**James Gosling**, **Mike Sheridan**, and **Patrick Naughton** initiated the Java language project in June 1991. The small team of sun engineers called **Green Team**.

Java is a **programming language** and a **platform**. Java is a high level, robust, object-oriented and secure programming language.

Java was developed by *Sun Microsystems* (which is now the subsidiary of Oracle) in the year 1995. *James Gosling* is known as the father of Java. Before Java, its name was *Oak*. Since Oak was already a registered company, so James Gosling and his team changed the Oak name to Java.

**Platform**: Any hardware or software environment in which a program runs, is known as a platform. Since Java has a runtime environment (JRE) and API, it is called a platform.

#### Types of applications

1. Standalone
2. Web application
3. Enterprise application
4. Mobile application

#### Java Platforms Editions

1. Java SE (Java Standard Edition)
2. Java EE (Java Enterprise Edition)
3. Java ME (Java Micro Edition)
4. Java FX

#### Features of Java

1. **Simple**

   Java is very easy to learn, and its syntax is simple, clean and easy to understand

2. **Object-oriented**

   Java is an object-oriented programming language. Everything in Java is an object. Object-oriented means we organize our software as a combination of different types of objects that incorporates both data and behavior.

   Basic concepts of OOPs are: **Object, Class, Inheritance, Polymorphism, Abstraction, Encapsulation**

3. **Portable**

   Java is portable because it facilitates you to carry the Java bytecode to any platform. It doesn't require any implementation.

4. **Platform independent**

   Java code can be run on multiple platforms, for example, Windows, Linux, Sun Solaris, Mac/OS, etc. Java code is compiled by the compiler and converted into bytecode. This bytecode is a platform-independent code because it can be run on multiple platforms, i.e., Write Once and Run Anywhere(WORA).

   The Java platform differs from most other platforms in the sense that it is a software-based platform that runs on the top of other hardware-based platforms. It has two components:

   1. Runtime Environment
   2. API(Application Programming Interface)

5. **Secured**

   Java is best known for its security. With Java, we can develop virus-free systems. Java is secured because:

   - No explicit pointer
   - Java Programs run inside a virtual machine sandbox
   - **Classloader:** Classloader in Java is a part of the Java Runtime Environment(JRE) which is used to load Java classes into the Java Virtual Machine dynamically. It adds security by separating the package for the classes of the local file system from those that are imported from network sources.
   - **Bytecode Verifier:** It checks the code fragments for illegal code that can violate access right to objects.
   - **Security Manager:** It determines what resources a class can access such as reading and writing to the local disk.

6. **Robust**

   Robust simply means strong. Java is robust because:

   - It uses strong memory management.
   - There is a lack of pointers that avoids security problems.
   - There is automatic garbage collection in java which runs on the Java Virtual Machine to get rid of objects which are not being used by a Java application anymore.
   - There are exception handling and the type checking mechanism in Java. All these points make Java robust.

7. **Architecture neutral**

   Java is architecture neutral because there are no implementation dependent features, for example, the size of primitive types is fixed.

   In C programming, int data type occupies 2 bytes of memory for 32-bit architecture and 4 bytes of memory for 64-bit architecture. However, it occupies 4 bytes of memory for both 32 and 64-bit architectures in Java.

8. **Interpreted**

9. **High performance**

   Java is faster than other traditional interpreted programming languages because Java bytecode is "close" to native code. It is still a little bit slower than a compiled language (e.g., C++). Java is an interpreted language that is why it is slower than compiled languages, e.g., C, C++, etc.

10. **Multithread**

    A thread is like a separate program, executing concurrently. We can write Java programs that deal with many tasks at once by defining multiple threads. 

11. **Distributed**

    Java is distributed because it facilitates users to create distributed applications in Java. **RMI** and **EJB** are used for creating distributed applications.

12. **Dynamic**

    Java is a dynamic language. It supports dynamic loading of classes. It means classes are loaded on demand. It also supports functions from its native languages, i.e., C and C++.

    Java supports dynamic compilation and automatic memory management (garbage collection).



#### C++ vs Java

| Comparison Index                        | C++                                                          | Java                                                         |
| :-------------------------------------- | :----------------------------------------------------------- | :----------------------------------------------------------- |
| **Platform-independent**                | C++ is platform-dependent.                                   | Java is platform-independent.                                |
| **Mainly used for**                     | C++ is mainly used for system programming.                   | Java is mainly used for application programming. It is widely used in window, web-based, enterprise and mobile applications. |
| **Design Goal**                         | C++ was designed for systems and applications programming. It was an extension of C programming language. | Java was designed and created as an interpreter for printing systems but later extended as a support network computing. It was designed with a goal of being easy to use and accessible to a broader audience. |
| **Goto**                                | C++ supports the goto statement.                             | Java doesn't support the goto statement.                     |
| **Multiple inheritance**                | C++ supports multiple inheritance.                           | Java doesn't support multiple inheritance through class. It can be achieved by interfaces in java. |
| **Operator Overloading**                | C++ supports operator overloading.                           | Java doesn't support operator overloading.                   |
| **Pointers**                            | C++ supports pointers. You can write pointer program in C++. | Java supports pointer internally. However, you can't write the pointer program in java. It means java has restricted pointer support in java. |
| **Compiler and Interpreter**            | C++ uses compiler only. C++ is compiled and run using the compiler which converts source code into machine code so, C++ is platform dependent. | Java uses compiler and interpreter both. Java source code is converted into bytecode at compilation time. The interpreter executes this bytecode at runtime and produces output. Java is interpreted that is why it is platform independent. |
| **Call by Value and Call by reference** | C++ supports both call by value and call by reference.       | Java supports call by value only. There is no call by reference in java. |
| **Structure and Union**                 | C++ supports structures and unions.                          | Java doesn't support structures and unions.                  |
| **Thread Support**                      | C++ doesn't have built-in support for threads. It relies on third-party libraries for thread support. | Java has built-in thread support.                            |



#### Difference between JDK, JRE, and JVM

**JVM**

JVM (Java Virtual Machine) is an abstract machine. It is called a virtual machine because it doesn't physically exist. It is a specification that provides a runtime environment in which Java bytecode can be executed.

JVMs are available for many hardware and software platforms. JVM, JRE, and JDK are platform dependent because the configuration of each OS is different from each other. However, Java is platform independent. There are three notions of the JVM: *specification*, *implementation*, and *instance*.

The JVM performs the following main tasks:

- Loads code
- Verifies code
- Executes code
- Provides runtime environment

**JVM Architecture**

It contains **classloader, memory area, execution engine, java native libraries**.

1. **Classloader**

   It is a subsystem of JVM which is used to load class file. Whenever we run the java program, it is loaded first by the classloader. There are three built-in classloaders in Java.

   1. **Bootstrap ClassLoader**: This is the first classloader which is the super class of Extension classloader. It loads the *rt.jar* file which contains all class files of Java Standard Edition like java.lang package classes, java.net package classes, java.util package classes, java.io package classes, java.sql package classes etc.

   2. **Extension ClassLoader**: This is the child classloader of Bootstrap and parent classloader of System classloader. It loads the jar files located inside *$JAVA_HOME/jre/lib/ext* directory.

   3. **System/Application ClassLoader**: This is the child classloader of Extension classloader. It loads the classfiles from classpath. By default, classpath is set to current directory. You can change the classpath using "-cp" or "-classpath" switch. It is also known as Application classloader.

      

2. **Memory Ares allocated by JVM**

   1. **Class(Method) Area**

      Class(Method) Area stores per-class structures such as the runtime constant pool, field and method data, the code for methods.

   2. **Heap**

      It is the runtime data area in which objects are allocated.

   3. **Stack**

      Java Stack stores frames. It holds local variables and partial results, and plays a part in method invocation and return.

      Each thread has a private JVM stack, created at the same time as thread.

      A new frame is created each time a method is invoked. A frame is destroyed when its method invocation completes.

   4. **Program Counter Register**

      PC (program counter) register contains the address of the Java virtual machine instruction currently being executed.

   5. **Native Method Stack**

      It contains all the native methods used in the application.

      

3. **Execution Engine**

   It contains

   1. A virtual processor

   2. Interpreter

   3. JIT (Just-In-Time) - It is used to improve the performance. JIT compiles parts of the byte code that have similar functionality at the same time, and hence reduces the amount of time needed for compilation.

      

4. **Java Native Interface**

   Java Native Interface (JNI) is a framework which provides an interface to communicate with another application written in another language like C, C++, Assembly etc. Java uses JNI framework to send output to the Console or interact with OS libraries.



**JRE**

JRE is an acronym for Java Runtime Environment. The Java Runtime Environment is a set of software tools which are used for developing Java applications. It is used to provide the runtime environment. It is the implementation of JVM. It physically exists. It contains a set of libraries + other files that JVM uses at runtime.

``The implementation of JVM is also actively released by other companies besides Sun Micro Systems.``



**JDK**

JDK is an acronym for Java Development Kit. The Java Development Kit (JDK) is a software development environment which is used to develop Java applications and applets. It physically exists. It contains JRE + development tools.

JDK is an implementation of any one of the below given Java Platforms released by Oracle Corporation:

- Standard Edition Java Platform
- Enterprise Edition Java Platform
- Micro Edition Java Platform

The JDK contains a private Java Virtual Machine (JVM) and a few other resources such as an interpreter/loader (java), a compiler (javac), an archiver (jar), a documentation generator (Javadoc), etc. to complete the development of a Java Application.