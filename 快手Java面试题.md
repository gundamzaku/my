## volatile 是什么？有什么用？它的主要应用场景是什么？
## transient关键字是什么意思
java语言的关键字，变量修饰符，如果用transient声明一个实例变量，当对象存储时，它的值不需要维持。换句话来说就是，用transient关键字标记的成员变量不参与序列化过程。
```JAVA
class Test {
  transient int a; // 不会被持久化
  int b; // 持久化
}
```
当类Test的实例对象被序列化（比如将Test类的实例对象 t 写入硬盘的文本文件t.txt中），变量 a 的内容不会被保存，变量 b 的内容则会被保存。

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
桶排序的原理是：将数组分到有限数量的桶子里。每个桶子再个别排序（有可能再使用别的排序算法或是以递归方式继续使用桶排序进行排序）。桶排序是鸽巢排序的一种归纳结果。当要被排序的数组内的数值是均匀分配的时候，桶排序使用线性时间（Θ（n））。但桶排序并不是 比较排序，他不受到 O(n log n) 下限的影响。主要原理是：利用了空间换时间的方法。

## ConcurrentHashMap有什么特点？和HashMap比有什么优势？ConcurrentHashMap的数据结构和HashMap有什么区别？put和get方法是怎么实现的？
ConcurrentHashMap融合了hashtable和hashmap二者的优势。  
但是hashtable每次同步执行的时候都要锁住整个结构  
hashtable是做了同步的，hashmap未考虑同步。所以hashmap在单线程情况下效率较高。hashtable在的多线程情况下，同步操作能保证程序执行的正确性  
ConcurrentHashMap锁的方式是稍微细粒度的。 ConcurrentHashMap将hash表分为16个桶（默认值）  

## Nio的机制是什么？解释一下Nio？
## 当一个用户在浏览器中输入baidu.com之后，这其中都发生了什么？
1. DNS域名解析  
2. 建立TCP连接  
3. 发起HTTP请求  
4. 接受响应结果  
5. 浏览器解析html  
6. 浏览器布局渲染  
