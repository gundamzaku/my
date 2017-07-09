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

    public static void sayHello(){
        System.out.println("hello world");
    }

    public static void main(String[] args){
        StaticResolution.sayHello();
    }
}
```

去class生成的目录执行
javap -verbose StaticResolution  

result:

```java 
Compiled from "StaticResolution.java"
public class StaticResolution {
  public StaticResolution();
  public static void sayHello();
  public static void main(java.lang.String[]);
}
mac:nio liudan$ javap -verbose StaticResolution
Classfile /Users/liudan/Documents/code/nio/out/production/nio/StaticResolution.class
  Last modified 2017-7-9; size 618 bytes
  MD5 checksum 0596e808e357cc74a0860d6e77ac772a
  Compiled from "StaticResolution.java"
public class StaticResolution
  SourceFile: "StaticResolution.java"
  minor version: 0
  major version: 51
  flags: ACC_PUBLIC, ACC_SUPER
Constant pool:
   #1 = Methodref          #7.#22         //  java/lang/Object."<init>":()V
   #2 = Fieldref           #23.#24        //  java/lang/System.out:Ljava/io/PrintStream;
   #3 = String             #25            //  hello world
   #4 = Methodref          #26.#27        //  java/io/PrintStream.println:(Ljava/lang/String;)V
   #5 = Methodref          #6.#28         //  StaticResolution.sayHello:()V
   #6 = Class              #29            //  StaticResolution
   #7 = Class              #30            //  java/lang/Object
   #8 = Utf8               <init>
   #9 = Utf8               ()V
  #10 = Utf8               Code
  #11 = Utf8               LineNumberTable
  #12 = Utf8               LocalVariableTable
  #13 = Utf8               this
  #14 = Utf8               LStaticResolution;
  #15 = Utf8               sayHello
  #16 = Utf8               main
  #17 = Utf8               ([Ljava/lang/String;)V
  #18 = Utf8               args
  #19 = Utf8               [Ljava/lang/String;
  #20 = Utf8               SourceFile
  #21 = Utf8               StaticResolution.java
  #22 = NameAndType        #8:#9          //  "<init>":()V
  #23 = Class              #31            //  java/lang/System
  #24 = NameAndType        #32:#33        //  out:Ljava/io/PrintStream;
  #25 = Utf8               hello world
  #26 = Class              #34            //  java/io/PrintStream
  #27 = NameAndType        #35:#36        //  println:(Ljava/lang/String;)V
  #28 = NameAndType        #15:#9         //  sayHello:()V
  #29 = Utf8               StaticResolution
  #30 = Utf8               java/lang/Object
  #31 = Utf8               java/lang/System
  #32 = Utf8               out
  #33 = Utf8               Ljava/io/PrintStream;
  #34 = Utf8               java/io/PrintStream
  #35 = Utf8               println
  #36 = Utf8               (Ljava/lang/String;)V
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

  public static void sayHello();
    flags: ACC_PUBLIC, ACC_STATIC
    Code:
      stack=2, locals=0, args_size=0
         0: getstatic     #2                  // Field java/lang/System.out:Ljava/io/PrintStream;
         3: ldc           #3                  // String hello world
         5: invokevirtual #4                  // Method java/io/PrintStream.println:(Ljava/lang/String;)V
         8: return        
      LineNumberTable:
        line 7: 0
        line 8: 8

  public static void main(java.lang.String[]);
    flags: ACC_PUBLIC, ACC_STATIC
    Code:
      stack=0, locals=1, args_size=1
         0: invokestatic  #5                  // Method sayHello:()V
         3: return        
      LineNumberTable:
        line 11: 0
        line 12: 3
      LocalVariableTable:
        Start  Length  Slot  Name   Signature
               0       4     0  args   [Ljava/lang/String;
}
```
