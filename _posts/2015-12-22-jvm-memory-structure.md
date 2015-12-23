---
layout: post
title: JVM Memory Structure
cover: tree.jpg
date:   2015-12-22 22:00:00
categories: posts
---
## JVM MEMORY STRUCTURE
The JVM memory consists of the following segments:
* Heap Memory, which is the storage for Java objects
* Non-Heap Memory, which is used by Java to store loaded classes and other meta-data
* JVM code itself, JVM internal structures, loaded profiler agent code and data, etc.

##Heap
The JVM has a heap that is the runtime data area from which memory for all class instances and arrays are allocated. It is created at the JVM start-up.

* -Xmx<size> - to set the maximum Java heap size
* -Xms<size> - to set initial Java heap size

By default, the maximum heap is 64Mb.

##Non-Heap
Also, the JVM has memory other than the heap, referred to as non-heap memory. It is created at the JVM startup and stores per-class structures such as runtime constant pool, field and method data, and the code for methods and constructors, as well as interned Strings.

Unfortunately, the only information JVM provides on non-heap memory is its overall size. No detailed information on non-heap memory content is available.

The abnormal growth of non-heap memory size may indicate a potential problem, in this case you may check up the following:

If there are class loading issues such as leaked loaders. In this case, the problem may be solved with the help of Class loaders view.
If there are strings being massively interned. For detection of such problem, Object allocation recording may be used.

If the application indeed needs that much of non-heap memory and the default maximum size of 64 Mb is not enough, you may enlarge the maximum size with the help of -XX:MaxPermSize VM option. 
For example, -XX:MaxPermSize=128m sets the size of 128 Mb.

