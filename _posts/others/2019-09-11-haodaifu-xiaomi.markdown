---
layout:     post
title:      "review "
date:       2019-09-11 
categories: Other
tags: Blog
---





笔试：

#### 1.悲观锁和乐观锁？

悲观锁：就是很悲观认为在拿数据的时候，别人会修改数据。所以每次拿数据要先上锁，别人使用数据需要等到拿到锁。适用于不同用户使用数据时，发生冲突概率高的情况。

乐观锁: 认为自己在使用时，别人不会修改数据，所以没有锁。若发生冲突，上层应用进行retry。

**实现方式**：

悲观锁实现方式是加锁，比如Java中的syn chro nized，（数据也可以加锁，MySQL排他锁）

乐观锁：CAS机制， 版本号机制 实现

2. #### CAS机制？

    CAS机制（Compare And Swap）是比较并交换的意思，CAS使用了3个操作数：内存地址V,旧的预期值A和新的变量B。在更新变量时，只有当V和旧的预期值A相等时，才更新成新的值B。
   
    比如内存地址存储着V=10的变量，当线程1想将变量值增加1，对应线程1来说旧的预期值A=10，想要改成新的B=11；  线程2先一步将内存地址的值改成了11，这时线程1通过比较后当前的V和旧的预期值A=10不相等,更新就失败了。要等到线程1获取V=11的值后，重新计算预期值A=11（自旋）.
优点：性能比 Synchronized关键字好
缺点：(1)ABA问题：线程1读取A;线程2修改成B；线程2修改成A，线程1做操作，在栈操作时会导致栈发生变化 （2）在高竞争条件下，CSA会反复失败，CPU的开销较大 （3）因为是对 单一变量做比较替换，不能保证代码块的原子性。

**乐观锁加锁吗？**
乐观锁本身是不加锁的，只在更新时判断一下数据是否被其他线程修改了；比如AtomicInteger

乐观锁可以与加锁操作一起合作加锁





1. MySQL存储引擎

   ​     数据库表是是用来存储数据的，而不同类型的表在查找、删除等性能上有差异，因此针对不同应用情况有不同的存储引擎（表）。里面的索引是基于Hash表或者B+树实现的

   

> 常见的存储引擎：
>
>  **MyIsam ：**独立于操作系统，在筛选大量数据时非常迅速，并发插入的特性允许同时选择和插入数据。例如：MyISAM存储引擎很适合管理邮件或Web服务器日志数据。
>
>  InnoDB： MySQL的默认引擎，有较高的并发读取频率，优点：事务（增删改），支持热备份，自动故障恢复，多版本并发控制
>


1. JVM在不同平台上运行的实现方式？
    Java语言具有“一次编译，到处执行”的特征，在不同平台上运行主要是通过.class文件和JVM实现的。Java源码在编译后生成 .class文件，.class存放的是字节码指令，不同平台的JVM负责将字节码指令翻译成机器码，由于平台不同，执行的机器码也不一样。


2. Java集合有哪些是线程安全的，
   线程安全    ：Vector、LikedList、StringBuffer、HashTable
   线程不安全：ArrayList、StringBuild、HashMap、HashSet
   线程安全的实现方式是对内部的方法都加了锁，synchronized
>Vector比ArrayList多一个同步机制，HashTable比HashMap多个线程安全，HashMap可放空值

3. 哈夫曼数，树的查找效率？
   哈夫曼数是带权路径长度最短的二叉树 ，构造方式：每次选权值最小两个节点作为叶节点（权值小的为左叶子节点），构造父节点。从生成的父节点和剩下的节点选权值最小的节点，重复刚才的过程，知道哈夫曼树构建完成。
   哈夫曼编码：按照不同字符出现的频率分配权值，按照字符的权值构建哈夫曼数。每个节点的左边标记为0，右边为1。每个字符按照根节点到叶子节点的二进制数进行编码。非定长编码。

   树：树结构查找效率高，可达到O(logn)，还可以保持有序。
   
4. B树

   考虑到 磁盘IO ，B数的查找效率更高 

   二叉查找数查找效率都很高，但数据量大的时候，索引不能全部加装到内存里，只能逐一加载磁盘页（磁盘页对应索引节点）。如果用二叉搜索树查找，最大的磁盘IO 次数等于节点的高度，为了减少IO次数，用“矮胖”的B树。

   多路径平衡查找树，子节点最多有K个，那该节点的元素最多K-1个

   > k是B树的阶，根据磁盘页大小来定，

   实际应用：文件系统和数据库索引，如非关系型数据库MongoDB

   > B-树（叫B树，- 不是减号）

5. B+树

   B+树特点：父节点元素都出现在子节点中（是子节点最小或最大的元素），因此所有叶子节点包括所有的元素。并且叶子节点指向下一个节点，叶子节点形成了一个有序的链表。另外一个特点是B+树只有叶子节点有卫星数据（数据具体的值），B树所有节点都有值，由于这个特点，相同磁盘页存放的B+树的索引更多，因此查询到叶子节点时，IO次数更少，性能更稳定（必须到叶子节点才结束）。B+树范围查找方便，直接在叶子节点的链表上查找

   ![](https://lukkyy.github.io/assets/other/Btree.png)

   > B 树和B+树的节点是索引

#### 





---

小米笔试2：

1.二叉树深度：就是二叉树的层数，只有一个根节点深度为1

2.中序：mnyxzp 后序为mxynpz 求前序?

后序最后一个字符是根节点，根据中序分成mnyx 和 zp两个子节点，递归这个步骤

判别式模型：

bagging bosting

集成模型和基本模型的关系

k-mean的O（）是多少，

ROC曲线和PR曲线

blending

编程题：

求数组子串和最大连续子串，对应letcode53，

System.in System.out 输出，输出还不会，需要去牛客网招模板

找真题刷，看面经的题目。

***



面经总结：

#### 

保证线程同步的三种方法

1、不在线程之间共享状态变量。
2、将状态变量改为不可变。
3、访问状态变量时使用同步。



AtomicInteger的实现原理，自己简单实现一下AtomicInteger中的increase()方法？

Java原子操作类？

Java.util.concurrent.atomic包下的类，AtomicInteger，AtomicLong

 `synchronized` 关键字使得没有得到，代价是昂贵的，多个线程之间访问同一个方法是互斥的，

```java
class Chenmo {
    private int lineCount = 0;
    private int wordCount = 0;
        synchronized (this) {
            lineCount++;
            wordCount++;
        }
    }
}
```

给两个方法的代码进行加锁，保证代码块的原子性的。

首先来介绍`AtomicInteger`。`java.util.concurrent.atomic.AtomicInteger` 是一个提供原子操作的 Integer 类，利用CPU提供的CAS操作来保证原子性；



```
System.out.println(3|9);  
11 //（二进制）
```