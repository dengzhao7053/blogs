---
title: "对象的创建"
date: 2020-03-30T11:51:37+08:00
categories: ["Java"]
tags: ["java"]
---
`Java`是一门面向对象的编程语言，`Java`程序运行过程中无时无刻都有对象被创建出来。在语言层面上，创建对象通常（例外：复制、反序列化）仅仅是一个`new`关键字而已，而在虚拟机中，普通`Java`对象的创建又是怎样一个过程呢？
<!--more-->

`Java`对象的创建包含以下几步：

### 1.判断对象对应的类是否加载、链接和初始化

当`Java`虚拟机遇到一条字节码`new`指令时，首先先检查这个指令的参数是否能在常量池中定位到一个类的符号引用，并且检查这个符号引用代表的类是否已经被加载、解析和初始化过。如果没有，那必须先执行相应的类加载过程。这部分细节将在后续的文章中呈现。

### 2.为对象分配内存

在类加载检查通过后，接下来虚拟机将为新生对象分配内存。对象所需内存的大小在类加载完成后便可以完全确定，为对象分配空间的任务实际上便是等同于把一块确定大小的内存块从`Java`堆中划分出来。内存分配根据`Java`堆是否规整，有两种方式：

①指针碰撞：如果`Java`堆的内存是规整的，即所有用过的内存放在一边，而空闲的内存放在另一边。分配内存时将位于中间的指针指示器向空闲的内存移动一段与对象大小相等的距离，这样便完成内存分配的工作

②空闲列表：如果`Java`堆内存不是规整的，则需要由虚拟机维护一个列表来记录哪些内存是可用的，这样在分配的时候可以从列表中查询到足够大的内存分配给对象，并在分配后更新列表记录。

`Java`堆的内存分配是否规整根据所采用的垃圾收集器是否带有压缩整理功能有关。

### 3.处理并发问题

除如何划分可用空间之外，还有另外一个需要考虑的问题：对象创建在虚拟机中是非常频繁的行为，即使仅仅修改一个指针所指向的位置，在并发情况下也并不是线程安全的，可能出现正在给对象A分配内存，指针还没来得及修改，对象B又同时使用了原来指针来分配内存的情况。解决这个问题有两种可选方案：

①对分配内存空间的动作进行同步处理，比如在虚拟机采用`CAS`算法并配上失败重试的方式保证更新操作的原子性。

②每个线程在`Java`堆中预先分配一小块内存，这块内存称为本地线程分配缓冲`(Thread Local Allocation Buffer, TLAB)`，线程需要分配内存时，就在对应线程的`TLAB`上分配内存，当线程中的`TLAB`用完并且被分配到了新的`TLAB`时，这时候才需要上述的同步锁定。

### 4.初始化零值

将分配到的内存，除了对象头外都初始化零值。这步操作保证了对象的实例字段在`Java`代码中可以不赋值就直接使用，使程序能访问到这些字段的数据类型所对应的零值。

### 5.设置对象头

将对象的所属类、对象的`hashcode`和对象的`GC`分代年龄等数据存储在对象的对象头中。

### 6.执行init方法进行初始化

执行`init`方法，初始化对象的成员变量、调用类的构造方法，这样一个对象就被创建了出来。