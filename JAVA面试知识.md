# 双亲委派  
# 设计模式  
重点两个设计模式
### 单例模式
### 工厂模式
```java
public class Factory{
    public static ISample creator(int which){
        if (which==1)
            return new SampleA();
        else if (which==2)
            return new SampleB();
    }
}以工厂的方式去调用对象
```
```Java
public abstract class Factory{
    public abstract Sample creator();
    public abstract Sample2 creator(String name);
}
public class SimpleFactory extends Factory{
    public Sample creator(){
        .........
        return new SampleA
    }
    public Sample2 creator(String name){
        .........
        return new Sample2A
    }
}
 
public class BombFactory extends Factory{
    public Sample creator(){
        ......
        return new SampleB
    }
    public Sample2 creator(String name){
        ......
        return new Sample2B
    }
} 抽象工厂模式
```
其它的设计模式还是要熟练掌握。

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
JVM内部的机制能够保证当一个类被加载的时候，这个类的加载过程是线程互斥的。  
这样第一次调用getInstance的时候，JVM能够保证instance只被创建一次，并且会保证把赋值给instance的内存初始化完毕。  
此外该方法也只会在第一次调用的时候使用互斥机制。  
最后instance是在第一次加载SingletonContainer类时被创建的。  
而SingletonContainer类则在调用getInstance方法的时候才会被加载，因此也实现了惰性加载。
```
# 幂等请求  
幂等性(Idempotence)
HTTP方法的幂等性是指一次和多次请求某一个资源应该具有同样的副作用。  
幂等性属于语义范畴，正如编译器只能帮助检查语法错误一样，HTTP规范也没有办法通过消息格式等语法手段来定义它。  
但实际上，幂等性是分布式系统设计中十分重要的概念，而HTTP的分布式本质也决定了它在HTTP中具有重要地位。

# zk,dubbo实现原理  
# 动态代理两种方式和区别  
```jdk动态代理```和```cglib动态代理```。
两种方法同时存在，各有优劣。
jdk动态代理是由Java内部的反射机制来实现的，cglib动态代理底层则是借助asm来实现的。
总的来说，反射机制在生成类的过程中比较高效，而asm在生成类之后的相关执行过程中比较高效
（可以通过将asm生成的类进行缓存，这样解决asm生成类过程低效问题）。
还有一点必须注意：jdk动态代理的应用前提，必须是目标类基于统一的接口。如果没有上述前提，jdk动态代理不能应用。
由此可以看出，jdk动态代理有一定的局限性，cglib这种第三方类库实现的动态代理应用更加广泛，且在效率上更有优势。。
［参考文章］(http://blog.csdn.net/heyutao007/article/details/49738887)
# 线程池四种区别  
### new Thread的弊端
性能差，功能少，缺少统一管理，容易混乱。
### 通过Executors提供四种线程池
```newCachedThreadPool```  
创建一个可缓存线程池，如果线程池长度超过处理需要，可灵活回收空闲线程，若无可回收，则新建线程。  
```newFixedThreadPool```  
创建一个定长线程池，可控制线程最大并发数，超出的线程会在队列中等待。  
```newScheduledThreadPool```  
创建一个定长线程池，支持定时及周期性任务执行。  
```newSingleThreadExecutor```  
创建一个单线程化的线程池，它只会用唯一的工作线程来执行任务，保证所有任务按照指定顺序(FIFO, LIFO, 优先级)执行。  

<b>线程池作用就是限制系统中执行线程的数量。</b>
# 二叉树层次遍历  
# future.get  
Future模式可以这样来描述：我有一个任务，提交给了Future，Future替我完成这个任务。  
期间我自己可以去做任何想做的事情。一段时间之后，我就便可以从Future那儿取出结果。  
就相当于下了一张订货单，一段时间后可以拿着提订单来提货，这期间可以干别的任何事情。  
其中Future 接口就是订货单，真正处理订单的是Executor类，它根据Future接口的要求来生产产品。
```java
ExecutorService executor = Executors.newSingleThreadExecutor();
FutureTask<String> future =
        new FutureTask<String>(new Callable<String>() {//使用Callable接口作为构造参数
            public String call() {
                return "hello world";
                //真正的任务在这里执行，这里的返回值类型为String，可以为任意类型
            }});
executor.execute(future);
String result = "";
//在这里可以做别的任何事情
try {
    result = future.get(5000, TimeUnit.MILLISECONDS); //取得结果，同时设置超时执行时间为5秒。同样可以用future.get()，不设置执行超时时间取得结果
} catch (InterruptedException e) {
    future.cancel(true);
} catch (ExecutionException e) {
    future.cancel(true); 
} catch (TimeoutException e) {
    future.cancel(true);
} finally {
    executor.shutdown();
}
System.out.println(result);
```
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
### 可重入锁
也叫做递归锁，指的是同一线程 外层函数获得锁之后 ，内层递归函数仍然有获取该锁的代码，但不受影响。  
在JAVA环境下 ```ReentrantLock``` 和```synchronized``` 都是 可重入锁  
举个简单的例子，当一个线程执行到某个synchronized方法时，比如说method1，而在method1中会调用另外一个synchronized方法method2，  
此时线程不必重新去申请锁，而是可以直接执行方法method2。
```Java
class MyClass {
    public synchronized void method1() {
        method2();
    }
     
    public synchronized void method2() {
         
    }
}
```
假如某一时刻，线程A执行到了method1，此时线程A获取了这个对象的锁，  
而由于method2也是synchronized方法，假如synchronized不具备可重入性，此时线程A需要重新申请锁。

### 读写锁
读写锁将对一个资源（比如文件）的访问分成了2个锁，一个读锁和一个写锁。  
正因为有了读写锁，才使得多个线程之间的读操作不会发生冲突。  
ReadWriteLock就是读写锁，它是一个接口，ReentrantReadWriteLock实现了这个接口。  
可以通过readLock()获取读锁，通过writeLock()获取写锁。
  
# 类的加载机制  
Class文件由类装载器装载后，在JVM中将形成一份描述Class结构的元信息对象，通过该元信息对象可以获知Class的结构信息：如构造函数，属性和方法等，Java允许用户借由这个Class相关的元信息对象间接调用Class对象的功能。  

虚拟机把描述类的数据从class文件加载到内存，并对数据进行校验，转换解析和初始化，最终形成可以被虚拟机直接使用的Java类型，这就是虚拟机的类加载机制。
