## volatile 是什么？有什么用？它的主要应用场景是什么？
## transient关键字是什么意思
java语言的关键字，变量修饰符，如果用transient声明一个实例变量，当对象存储时，它的值不需要维持。换句话来说就是，用transient关键字标记的成员变量不参与序列化过程。
```JAVA
public class UserInfo implements Serializable {
    private static final long serialVersionUID = 1L;
    private String name ;
    private transient String pwd ;
    public UserInfo(String name,String pwd){
        this.name =name;
        this.pwd =pwd;
    }
    public String toString(){
        return "name=" +name +",psw=" +pwd ;
    }
}
```
这是一个非常简单明了的例子。首先创造一个类，继承了Ｓerializable的接口。
其中的pwd补标记成transient。
```Java
public static void main(String[] args) {
    UserInfo userInfo = new UserInfo("张三" , "123456" );
    System. out.println(userInfo);
    try {
        // 序列化，被设置为transient的属性没有被序列化
        ObjectOutputStream o = new ObjectOutputStream(new FileOutputStream("UserInfo.out"));
        o.writeObject(userInfo);
        o.close();
    } catch (Exception e) {
        e.printStackTrace();
    }
    try {
        // 重新读取内容，这个时候被标记成transient的变量并不显示，已经没有被序列化进来。
        ObjectInputStream in = new ObjectInputStream( new FileInputStream("UserInfo.out"));
        UserInfo readUserInfo = (UserInfo) in.readObject();
        // 读取后psw的内容为null
        System. out.println(readUserInfo.toString());
    } catch (Exception e) {
        e.printStackTrace();   
    }
}
```

## 下段代码会发生什么
```Java
List<Integer> list1 = new ArrayList<>();
List list2 = list1;
list2.add("a");
list1.get(0);
list1.get(0);
Integer a = list.get(0);
```
这段代码有问题
## GC分代回收机制是什么？我们怎么确定一个对象是可以回收的？一个对象在回收的过程中如果发生了循环引用，JVM是怎么解决的？JAVA堆中的对象在回收的过程中具体发生了什么？新建立的对象是在堆的哪部分。
http://www.jianshu.com/p/ace2aa692f96  
http://www.jianshu.com/p/bfa5337ef59e  
http://www.jianshu.com/p/440b641c08cb  
http://www.jianshu.com/u/34eadc1d5303  
原理较多

## kafka是怎么保证数据稳健性的？当A机器得到消息但是挂掉之后是怎么确保这条数据的？
Apache Kafka是分布式发布-订阅消息系统。它最初由LinkedIn公司开发，之后成为Apache项目的一部分。Kafka是一种快速、可扩展的、设计内在就是分布式的，分区的和可复制的提交日志服务。

## HashMap的原理？桶的结构？扩容方法中新的桶的值有什么映射关系？桶中的一个链表的数据是怎么映射到新的map中去？
哈希表是由数组+链表组成的，一个长度为16的数组中，就是从hash(key)%len获得，也就是元素的key的哈希值对数组长度取模得到  
HashMap里面实现一个静态内部类Entry，其重要的属性有 key , value, next  
```Java
transient Entry[] table;
```
http://blog.csdn.net/vking_wang/article/details/14166593  

下面这篇文章已经解释的相当好了
http://www.importnew.com/10620.html

桶排序的原理是：将数组分到有限数量的桶子里。每个桶子再个别排序（有可能再使用别的排序算法或是以递归方式继续使用桶排序进行排序）。桶排序是鸽巢排序的一种归纳结果。当要被排序的数组内的数值是均匀分配的时候，桶排序使用线性时间（Θ（n））。但桶排序并不是 比较排序，他不受到 O(n log n) 下限的影响。主要原理是：利用了空间换时间的方法。

## ConcurrentHashMap有什么特点？和HashMap比有什么优势？ConcurrentHashMap的数据结构和HashMap有什么区别？put和get方法是怎么实现的？
ConcurrentHashMap融合了hashtable和hashmap二者的优势。  
但是hashtable每次同步执行的时候都要锁住整个结构  
hashtable是做了同步的，hashmap未考虑同步。所以hashmap在单线程情况下效率较高。hashtable在的多线程情况下，同步操作能保证程序执行的正确性  
ConcurrentHashMap锁的方式是稍微细粒度的。 ConcurrentHashMap将hash表分为16个桶（默认值）  

ConcurrentHashMap在线程安全的基础上提供了更好的写并发能力，但同时降低了对读一致性的要求。

ConcurrentHashMap的设计与实现非常精巧，大量的利用了volatile，final，CAS等lock-free技术来减少锁竞争对于性能的影响，无论对于Java并发编程的学习还是Java内存模型的理解，ConcurrentHashMap的设计以及源码都值得非常仔细的阅读与揣摩。

jdk1.8里面被重写了，用了很多算法。

HashTable的迭代器是强一致性的，而ConcurrentHashMap是弱一致的。

这里的弱一致性是指put操作将一个元素加入到底层数据结构后，get可能在某段时间内还看不到这个元素。实际应用中这方式有问题。

ConcurrentHashMap在写的时候用锁了，在读的时候并没有用锁。

这一篇讲得非常完善
http://blog.csdn.net/basycia/article/details/51890699


http://ifeve.com/java-concurrent-hashmap-1/
http://ifeve.com/java-concurrent-hashmap-2/

## Nio的机制是什么？解释一下Nio？
## 当一个用户在浏览器中输入baidu.com之后，这其中都发生了什么？
1. DNS域名解析  
2. 建立TCP连接  
3. 发起HTTP请求  
4. 接受响应结果  
5. 浏览器解析html  
6. 浏览器布局渲染  
