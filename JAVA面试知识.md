# 双亲委派  
# 设计模式  
# SSH实现原理、懒加载  
在开发中，如果某个实例的创建需要消耗很多系统资源，那么我们通常会使用惰性加载机制，也就是说只有当使用到这个实例的时候才会创建这个实例，这个好处在单例模式中得到了广泛应用。这个机制在single-threaded环境下的实现非常简单，然而在multi-threaded环境下却存在隐患。  
```Java
public static synchronized Singleton getInstance(){        
    if (instance == null)        
    instance = new Singleton();         
    return instance;         
}多线程下面的单例模式，加synchronized来控制，但是影响性能
```
```Java
public class Singleton{        
    private Singleton(){        
        …        
    }        
    private static class SingletonContainer{        
        private static Singleton instance = new Singleton();        
    }        
    public static Singleton getInstance(){        
        return SingletonContainer.instance;        
    }        
} 
JVM内部的机制能够保证当一个类被加载的时候，这个类的加载过程是线程互斥的。这样当我们第一次调用getInstance的时候，JVM能够帮我们保证instance只被创建一次，并且会保证把赋值给instance的内存初始化完毕。此外该方法也只会在第一次调用的时候使用互斥机制。最后instance是在第一次加载SingletonContainer类时被创建的，而SingletonContainer类则在调用getInstance方法的时候才会被加载，因此也实现了惰性加载。
```
# 幂等请求  
# zk,dubbo实现原理  
# 动态代理两种方式和区别  
# 线程池四种区别  
# 二叉树层次遍历  
# future.get  
# 微服务理解  
简单地说，Microservice架构模式就是将整个Web应用组织为一系列小的Web服务。  
这些小的Web服务可以独立地编译及部署，并通过各自暴露的API接口相互通讯。  
它们彼此相互协作，作为一个整体为用户提供功能，却可以独立地进行扩容。

# Mysql索引：聚族索引、非聚族索引  
最通俗的解释是:聚簇索引的顺序就是数据的物理存储顺序，而对非聚簇索引的索引顺序与数据物理排列顺序无关。  
简单解释，用字典。 
聚簇索引是直接翻字典，如果是安字，就知道是A，在字典前几页，直接去翻。  
非聚簇索引是先去查部首，然后定位到安字在第几页，然后去翻。  

# JVM内存使用过高  
参数调控堆、栈的大小（这个后面还是要好好研究一下）

# 可重入锁、读写锁概念  
# 类的加载机制  
Class文件由类装载器装载后，在JVM中将形成一份描述Class结构的元信息对象，通过该元信息对象可以获知Class的结构信息：如构造函数，属性和方法等，Java允许用户借由这个Class相关的元信息对象间接调用Class对象的功能。  

虚拟机把描述类的数据从class文件加载到内存，并对数据进行校验，转换解析和初始化，最终形成可以被虚拟机直接使用的Java类型，这就是虚拟机的类加载机制。
