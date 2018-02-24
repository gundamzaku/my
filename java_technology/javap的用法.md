javap是反编译，所以要去class生成的目录执行。  
javap常用参数  

```
-l 输出行及局部变量表。
-b 确保与 JDK 1.1 javap 的向后兼容性。
-public 只显示 public 类及成员。
-protected 只显示 protected 和 public 类及成员。
-package 只显示包、protected 和 public 类及成员。这是缺省设置。
-private 显示所有类和成员。
-J[flag] 直接将 flag 传给运行时系统。
-s 输出内部类型签名。
-c 输出类中各方法的未解析的代码，即构成 Java 字节码的指令。
-verbose 输出堆栈大小、各方法的 locals 及 args 数,以及class文件的编译版本
-classpath[路径] 指定 javap 用来查找类的路径。如果设置了该选项，则它将覆盖缺省值或 CLASSPATH 环境变量。目录用冒号分隔。
-bootclasspath[路径] 指定加载自举类所用的路径。缺省情况下，自举类是实现核心 Java 平台的类，位于 jrelibt.jar 和 jrelibi18n.jar 中。
-extdirs[dirs] 覆盖搜索安装方式扩展的位置。扩展的缺省位置是 jrelibext。
```

下面看一段实例  
```go
public class StaticResolution {

    public static void main(String[] args){

        String a = "hello";
        System.out.println(a);
    }
}
```

去class生成的目录执行
javap -verbose StaticResolution  

result:

```java 
Classfile /Users/liudan/Documents/code/nio/out/production/nio/StaticResolution.class
  Last modified 2017-7-9; size 586 bytes
  MD5 checksum ce7a890b2f967cce190fa29823354e34
  Compiled from "StaticResolution.java"
public class StaticResolution
  SourceFile: "StaticResolution.java"
  minor version: 0
  major version: 51
  flags: ACC_PUBLIC, ACC_SUPER
//常量池
Constant pool:
   #1 = Methodref          #6.#22         //  java/lang/Object."<init>":()V
   #2 = String             #23            //  hello
   #3 = Fieldref           #24.#25        //  java/lang/System.out:Ljava/io/PrintStream;
   #4 = Methodref          #26.#27        //  java/io/PrintStream.println:(Ljava/lang/String;)V
   #5 = Class              #28            //  StaticResolution
   #6 = Class              #29            //  java/lang/Object
   #7 = Utf8               <init>
   #8 = Utf8               ()V
   #9 = Utf8               Code
  #10 = Utf8               LineNumberTable
  #11 = Utf8               LocalVariableTable
  #12 = Utf8               this
  #13 = Utf8               LStaticResolution;
  #14 = Utf8               main
  #15 = Utf8               ([Ljava/lang/String;)V
  #16 = Utf8               args
  #17 = Utf8               [Ljava/lang/String;
  #18 = Utf8               a
  #19 = Utf8               Ljava/lang/String;
  #20 = Utf8               SourceFile
  #21 = Utf8               StaticResolution.java
  #22 = NameAndType        #7:#8          //  "<init>":()V
  #23 = Utf8               hello
  #24 = Class              #30            //  java/lang/System
  #25 = NameAndType        #31:#32        //  out:Ljava/io/PrintStream;
  #26 = Class              #33            //  java/io/PrintStream
  #27 = NameAndType        #34:#35        //  println:(Ljava/lang/String;)V
  #28 = Utf8               StaticResolution
  #29 = Utf8               java/lang/Object
  #30 = Utf8               java/lang/System
  #31 = Utf8               out
  #32 = Utf8               Ljava/io/PrintStream;
  #33 = Utf8               java/io/PrintStream
  #34 = Utf8               println
  #35 = Utf8               (Ljava/lang/String;)V
{
  public StaticResolution();
    flags: ACC_PUBLIC
    Code:
      stack=1, locals=1, args_size=1
         0: aload_0       
         1: invokespecial #1                  // Method java/lang/Object."<init>":()V
         4: return        
      LineNumberTable:
        line 4: 0
      LocalVariableTable:
        Start  Length  Slot  Name   Signature
               0       5     0  this   LStaticResolution;

  public static void main(java.lang.String[]);
    flags: ACC_PUBLIC, ACC_STATIC
    Code:
      stack=2, locals=2, args_size=1
         0: ldc           #2                  // String hello
         2: astore_1      
         3: getstatic     #3                  // Field java/lang/System.out:Ljava/io/PrintStream;
         6: aload_1       
         7: invokevirtual #4                  // Method java/io/PrintStream.println:(Ljava/lang/String;)V
        10: return        
      LineNumberTable:
        line 8: 0
        line 9: 3
        line 10: 10
      LocalVariableTable:
        Start  Length  Slot  Name   Signature
               0      11     0  args   [Ljava/lang/String;
               3       8     1     a   Ljava/lang/String;
}
```
