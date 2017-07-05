### channel
有五种：

FileChannel 从文件中读写数据。  
DatagramChannel 能通过UDP读写网络中的数据。  
SocketChannel 能通过TCP读写网络中的数据。  
ServerSocketChannel可以监听新进来的TCP连接，像Web服务器那样。对每一个新进来的连接都会创建一个SocketChannel。  

```java
import java.io.FileNotFoundException;
import java.io.IOException;
import java.io.RandomAccessFile;
import java.nio.ByteBuffer;
import java.nio.channels.FileChannel;
import java.nio.charset.CharacterCodingException;
import java.nio.charset.Charset;
import java.nio.charset.CharsetDecoder;

public class Main {

    public static void main(String[] args) throws FileNotFoundException {
        /*
         *Java.nio.charset.Charset处理了字符转换问题。
         * 它通过构造CharsetEncoder和CharsetDecoder将字符序列转换成字节和逆转换。
         */
        Charset charset = Charset.forName("GBK");
        CharsetDecoder decoder = charset.newDecoder();

        //这个文件在src的外面
        RandomAccessFile aFile = new RandomAccessFile("newiotxt", "rw");
        FileChannel fileChannel = aFile.getChannel();
        //以上方法将创建一个容量为48字节的ByteBuffer,如果发现创建的缓冲区容量太小,唯一的选择就是重新创建一个大小合适的缓冲区.
        ByteBuffer buf = ByteBuffer.allocate(2000);

        int bytesRead = 0;
        try {
            bytesRead = fileChannel.read(buf);
        } catch (IOException e) {
            e.printStackTrace();
        }
        System.out.println(bytesRead);
        while (bytesRead!=-1){
            System.out.println("Read "+bytesRead);
            buf.flip();//回绕缓冲区，回到缓存对
            try {
                decoder.decode(buf);
            } catch (CharacterCodingException e) {
                e.printStackTrace();
            }
            while(buf.hasRemaining()){

                System.out.print((char)buf.get());
            }
            buf.clear();
            try {
                bytesRead = fileChannel.read(buf);
            } catch (IOException e) {
                e.printStackTrace();
            }
        }
        try {
            aFile.close();
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```
http://ifeve.com/channels/  
http://blog.csdn.net/chuyouyinghe/article/details/51461082
