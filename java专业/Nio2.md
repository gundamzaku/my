## transFrom()

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
