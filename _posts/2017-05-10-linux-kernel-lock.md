---
title:  "Linux内核设计和实现-避免死锁的简单规则"
date:   2017-05-10 15:41:44
categories: LINUXKERNEL
---

**Basic**

《Linux内核设计和实现》书中提到了避免死锁的一些简单规则，具体如下：
 
 * 使用锁时要有针对性，要明确清楚需要保护的是数据而不是代码。针对代码加锁会使得程序难以理解，并且容易引发竞争条件，正确的做法应该是针对数据而不是代码加锁。
 * 按顺序加锁。使用嵌套的锁时必须保证以相同的顺序获取锁，这样可以阻止致命拥抱类型的死锁。最好能记录下锁的顺序，以便其他人也能照此顺序使用。
 * 防止发生饥饿。试问，这个代码的执行是否一定会结束？如果“张”不发生？“王”要一直等待下去吗？
 * 不要重复请求同一个锁。
 * 设计应力求简单---越复杂的加锁方案越有可能造成死锁。
