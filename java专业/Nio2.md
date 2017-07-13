## transFrom()
将字节从给定的可读取字节通道传输到此通道的文件中  
实例：
```java
    public static void main(String[] args) throws FileNotFoundException {
        RandomAccessFile fromFile = new RandomAccessFile("newiotxt", "rw");
        FileChannel      fromChannel = fromFile.getChannel();

        RandomAccessFile toFile = new RandomAccessFile("toFile.txt", "rw");
        FileChannel      toChannel = toFile.getChannel();

        long position = 0;
        long count = 0;
        try {
            count = fromChannel.size();
        } catch (IOException e) {
            e.printStackTrace();
        }
        System.out.println(100);
        count = 100;
        position = 5;//这个position是要写的文件的位置，不是newiotxt的位置
        try {
            toChannel.transferFrom(fromChannel,position, count);
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
```

## transferTo()
数据从FileChannel传输到其他的channel中
其实与上面的方法雷同。

## Selector
Selector（选择器）是Java NIO中能够检测一到多个NIO通道，并能够知晓通道是否为诸如读写事件做好准备的组件。这样，一个单独的线程可以管理多个channel，从而管理多个网络连接。

### 为什么使用Selector?
如果一个CPU有多个内核，不使用多任务可能是在浪费CPU能力。

### Selector的创建
```java
Selector selector = Selector.open();
```

### 向Selector注册通道
```java
channel.configureBlocking(false);
SelectionKey key = channel.register(selector,Selectionkey.OP_READ);
```

与Selector一起使用时，Channel必须处于非阻塞模式下。这意味着不能将FileChannel与Selector一起使用，因为FileChannel不能切换到非阻塞模式。而套接字通道都可以。

注意register()方法的第二个参数。这是一个“interest集合”，意思是在通过Selector监听Channel时对什么事件感兴趣。可以监听四种不同类型的事件：

Connect = SelectionKey.OP_CONNECT  
Accept = SelectionKey.OP_ACCEPT
Read = SelectionKey.OP_READ
Write = SelectionKey.OP_WRITE

如果你对不止一种事件感兴趣，那么可以用“位或”操作符将常量连接起来，如下：
```java
int interestSet = SelectionKey.OP_READ | SelectionKey.OP_WRITE;
```

### SelectionKey
当向Selector注册Channel时，register()方法会返回一个SelectionKey对象。这个对象包含了一些你感兴趣的属性：  

interest集合  
ready集合  
Channel  
Selector  
附加的对象（可选）  

#### interest集合
