---
layout: post
title: Welcome GitHub! I'm coming!
cover: cover.jpg
date:   2015-12-12 02:00:00
categories: posts
---

##Java Memory Model
The Java memory model specifies how the Java vritual machine works with the computer's memory (RAM).
It's import to understand Java memory model if you want to design correctly behaving concurrent programs. The Java memory model specifies how and when different threads can see values written to shared variables by other threads, and how to synchronize access to shared variables when necessary.

###The Internal Java Memory Model
The Java memory model used internally in the JVM divides memory between thread stacks and the heap.

Each thread running in the Java virtual machine has its own stack. The thread stack contains information about what methods the thread has called to reach the current point of excution. The thread stack contains all local variables for each method being excuted. A thread can only access it's own thread stack. Local variables created by a thread are invisible to all other threads than the thread who created it.

All local variables of primitive types ( boolean, byte, short, char, int, long, float, double) are fully stored on the thread stack and are thus not visible to other threads. One thread may pass a copy of a pritimive variable to another thread, but it cannot share the primitive local variable itself. 

The heap contains all objects created in your Java application, regardless of what thread created the object. This includes the object versions of the primitive types (e.g. Byte, Integer, Long etc.). It does not matter if an object was created and assigned to a local variable, or created as a member variable of another object, the object is still stored on the heap.

###JSR 133 - new Java Memory Model 
The new memory model semantics create a partial ordering on memory operations (read field, write field, lock, unlock) and other thread operations (start and join), where some actions are said to happen before other operations. When one action happens before another, the first is guaranteed to be ordered before and visible to the second. The rules of this ordering are as follows:

* Each action in a thread happens before every action in that thread that comes later in the program's order.
* An unlock on a monitor happens before every subsequent lock on that same monitor.
* A write to a volatile field happens before every subsequent read of that same volatile.
* A call to start() on a thread happens before any actions in the started thread.
* All actions in a thread happen before any other thread successfully returns from a join() on that thread.

When objects and variables can be stored in various different memory areas in the computer, certain problems may occur. The two main problems are: 
* Visibility of thread updates (writes) to shared variables.
* Race conditions when reading, checking and writing shared variables.

### Visibility of Shared Objects
If two or more threads are sharing an object, without the proper use of either volatile declarations or synchronization, updates to the shared object made by one thread may not be visible to other threads.To solve this problem you can use Java's volatile keyword. The volatile keyword can make sure that a given variable is read directly from main memory, and always written back to main memory when updated. 

### Race Conditions
If two or more threads share an object, and more than one thread updates variables in that shared object, race conditions may occur. To solve this problem you can use a Java synchronized block. A synchronized block guarantees that only one thread can enter a given critical section of the code at any given time. Synchronized blocks also guarantee that all variables accessed inside the synchronized block will be read in from main memory, and when the thread exits the synchronized block, all updated variables will be flushed back to main memory again, regardless of whether the variable is declared volatile or not.



