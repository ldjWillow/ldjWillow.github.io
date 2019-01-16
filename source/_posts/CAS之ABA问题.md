---
title: CAS之ABA问题
copyright: true
date: 2019-01-14 20:45:50
categories: 并发
tags: [CAS,并发]
---

###  CAS简介

CAS: Compare and Swap,比较并交换

java.util.concurrent包中借助CAS实现了区别于synchronous同步锁的一种乐观锁，使用这些类在多核CPU的机器上会有比较好的性能

CAS有3个操作，内存值V，旧的预期值A，要修改的新值B。当且仅当预期值A和内存值V相同时，将内存值V修改为B，否则什么都不做.

###  代码示例

```java
public class ABA {
    private static AtomicInteger atomicInt = new AtomicInteger(100);
    private static AtomicStampedReference atomicStampedRef = new AtomicStampedReference(100, 0);

    public static void main(String[] args) throws InterruptedException {
            Thread intT1 = new Thread(new Runnable() {
                    @Override
                    public void run() {
                      		//compareAndSet为原子操作方法A=100,B=101
                            atomicInt.compareAndSet(100, 101);
                            atomicInt.compareAndSet(101, 100);
                    }
            });

            Thread intT2 = new Thread(new Runnable() {
                    @Override
                    public void run() {
                            try {
                                    TimeUnit.SECONDS.sleep(1);
                            } catch (InterruptedException e) {
                            }
                            boolean c3 = atomicInt.compareAndSet(100, 101);
                            System.out.println(c3); // true
                    }
            });

            intT1.start();
            intT2.start();
            intT1.join();
            intT2.join();

            Thread refT1 = new Thread(new Runnable() {
                    @Override
                    public void run() {
                            try {	//休息1秒，让别的线程修改V的值
                                    TimeUnit.SECONDS.sleep(1);
                            } catch (InterruptedException e) {
                            }
                            atomicStampedRef.compareAndSet(100, 101, 				    atomicStampedRef.getStamp(), atomicStampedRef.getStamp() + 1);
                            atomicStampedRef.compareAndSet(101, 100, atomicStampedRef.getStamp(), atomicStampedRef.getStamp() + 1);
                    }
            });

            Thread refT2 = new Thread(new Runnable() {
                    @Override
                    public void run() {
                    	    //拿到版本号
                            int stamp = atomicStampedRef.getStamp();
                            try {
                            	    //休眠2秒，让别的线程修改版本号
                                    TimeUnit.SECONDS.sleep(2);
                            } catch (InterruptedException e) {
                            }
                            boolean c3 = atomicStampedRef.compareAndSet(100, 101, stamp, stamp + 1);
                            System.out.println(c3); // false
                    }
            });

            refT1.start();
            refT2.start();
    }
}
```

###  源码分析

- AtomicInteger

```java
 	// setup to use Unsafe.compareAndSwapInt for updates
    private static final Unsafe unsafe = Unsafe.getUnsafe();
    //用来记录value本身在内存中的内存地址，这个记录，也主要是为了在更新操作在内存中找到value的位置，方便	比较。
    private static final long valueOffset;
    //用来存储当前的值，声明为volatile，是为了保证在更新操作时，当前线程可以拿到value的最新的值(并发情		况下，value可能已经被其他线程更新了)
    private volatile int value;


public final boolean compareAndSet(int expect, int update) {
        //使用unsafe的本地方法，实现高效的硬件级别CAS
        return unsafe.compareAndSwapInt(this, valueOffset, expect, update);
 }
  public final int getAndSet(int newValue) {
        //自旋锁
        for (;;) {
            //获取在当前线程中的值
            int current = get();
            if (compareAndSet(current, newValue))
                return current;
        }
    }


```

- AtomicStampedReference

```java
//比较设置 参数依次为：期望值 写入新值 期望时间戳 新时间戳
public boolean compareAndSet(V expectedReference,V  
newReference,int expectedStamp,int newStamp)
//获得当前对象引用
public V getReference()
//获得当前时间戳
public int getStamp()
//设置当前对象引用和时间戳
public void set(V newReference, int newStamp)
```

### 参考链接

[AtomicInteger、Unsafe类、ABA问题](https://blog.csdn.net/wsyw126/article/details/53979918)

[[ava CAS 和ABA问题](https://www.cnblogs.com/549294286/p/3766717.html)](https://www.cnblogs.com/549294286/p/3766717.html)

[什么是CAS机制？](https://blog.csdn.net/qq_32998153/article/details/79529704)