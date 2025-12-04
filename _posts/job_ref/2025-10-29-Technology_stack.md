---
layout:     post
title:      "技术栈.25"
subtitle:   " \"Technology stack\""
date:       2025-10-29 19:30:00
author:     "LanZinYtt"
header-img: ""
catalog: true
tags:
    - Thread
---

<p id = "build"></p>

## 线程安全单例模式

### 1. 问题所在

**单例模式**是软件开发中最常用的设计模式之一。**它确保一个类在整个应用程序生命周期中只有一个实例，并提供全局访问点。**

   单例模式的典型应用场景包括：

   - 高效管理有限数据库连接的数据库连接池
   - 集中应用日志功能的日志实例
   - 存储应用级配置的配置管理器
   - 在多个组件间维护共享数据的缓存管理器
   - 管理并发操作工作线程的线程池

   但在多线程环境中实现单例模式时，事情会变得复杂。没有适当的线程安全保证，多个线程可能**同时创建多个实例**，破坏单例的核心承诺，并可能**导致资源冲突或状态不一致**。这会导致资源冲突、状态不一致和不可预测的应用行为。

### 2. 解决方法
**1. 同步访问器：简单安全**
```java
public static synchronized SynchronizedSingleton getInstance() {
    if (instance == null) {
        instance = new SynchronizedSingleton();
    }
    return instance;
}
```
- 对于每个instance的申请都使用synchronized进行同步。
- 这保证了**互斥**，但引入了**性能开销**，因为每次访问都会进行同步。
- 这种方法简单直接，在低并发场景或单例创建很少被访问的情况下很有效。

**2. 饿汉初始化：通过类加载保证线程安全**
```java
public class EagerSingleton {
    private static final EagerSingleton INSTANCE = new EagerSingleton();//使用static在类中直接创建
    
    private EagerSingleton() {}
    
    public static EagerSingleton getInstance() {
        return INSTANCE;
    }
}
```
- 它本质上是线程安全的，因为JVM保证类初始化是原子操作。
- 缺点是什么？即使从未使用，实例也会被创建，这对于昂贵资源可能不是最优选择
- 当单例保证在启动时就需要时，这种模式是理想选择。

**3. 双重检查锁定(DCL)：延迟且高效**
```java
public class DoubleCheckedSingleton {
    private static volatile DoubleCheckedSingleton instance;//使用volatile修饰
    
    private DoubleCheckedSingleton() {}
    
    public static DoubleCheckedSingleton getInstance() {
        if (instance == null) {
            synchronized (DoubleCheckedSingleton.class) {
                if (instance == null) {
                    instance = new DoubleCheckedSingleton();
                }
            }
        }
        return instance;
    }
}
```
- 这种模式既延迟又线程安全，但需要将实例变量声明为volatile
- 这种方法通过在实例初始化后避免同步来提高性能。volatile关键字确保跨线程的更改可见性。它适用于性能重要的高并发环境。

**4. Bill Pugh单例：延迟且优雅**
```java
public class BillPughSingleton {
    private BillPughSingleton() {
    }
    
    private static class SingletonHelper {
        private static final BillPughSingleton BILL_PUGH_SINGLETON_INSTANCE = new BillPughSingleton();
    }
    
    public static BillPughSingleton getInstance() {
        return SingletonHelper.BILL_PUGH_SINGLETON_INSTANCE;
    }
}
```
- 该类在系统引用它之前不会被加载，这确保了延迟和线程安全，无需同步

**5. 枚举单例：最简单的线程安全单例**
```java
public enum EnumSingleton {
    INSTANCE;
    
    public void performOperation() {
        // 单例操作在这里
    }
}
```
- Java在加载枚举时只实例化枚举常量一次，确保它们本质上是线程安全的
- 防止序列化和反射攻击

## Dubbo

## MQ消息队列

### 参考：
[Java线程安全单例模式实现指南](https://www.baeldung-cn.com/java-implement-thread-safe-singleton)