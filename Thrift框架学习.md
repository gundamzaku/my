## 发展的历程
从 数据访问框架(ORM) -> Web框架(MVC) -> 分布式服务框架(RPC)  -> 资源调度和治理中心(SOA)
主要解决的是千万级用户量的处理。

## 安装
http://maven.apache.org/download.cgi
在windows的环境变量中配置

mvn install -Dmaven.test.skip=true来尝试编译一下项目（并将jar安装到本地maven库）
似乎不用这么复杂，直接去MAVEN上下载即可？

yum install automake libtool flex bison pkgconfig gcc-c++ boost-devel libevent-devel zlib-devel python-devel ruby-devel  
yum -y install openssl openssl-devel  

最后的安装是用`./configure --disable-tests --disable-tutorial`完成的

` ./bootstrap.sh`在下载的包里面没有，是于git库上clone下来的source里面copy过去再执行的，很奇怪  
`./configure --with-boost-libdir=/usr/local/lib`之前用过这个命令，是因为boost默认的安装目录是在这里。  
而thrift编译的时候似乎是从lib64中去拿的。  
之前有报`libboost_unit_test_framework`的错误，是因为boost没装的关系，尽管yum里面显示已经装了，所以下载source重新自己装一次。  
`./bootstrap.sh`->`./b2 install`  
大至上就这么多，另外记得需要有足够的内够，不然也会报错。  
参考网址：http://thrift.apache.org/docs/install/

## 开始使用
首先，新建一个文件，比如hello.thrift  
用`thrift --gen java hello.thrift` 生成一套代码

具体可以参考
http://thrift.apache.org/tutorial/java
这里有生成报错Warning没关系，不要管。
已经非常详细了，不过注意的是里面的`CalculatorHandler`文件是不存在的，可以在http://thrift.apache.org/得到。  

编译器用maven的方式安装thrift

执行SharedServer，编译后报错`Could not load file: ../../lib/java/test/.keystore`

需要用到keytool工具来生成密钥
<b>私钥</b>
`keytool -genkeypair -alias certificatekey -keyalg RSA -validity 36500 -keystore .keystore`

<b>公钥</b>
`keytool -export -alias certificatekey -keystore .keystore -rfc -file server.cer`

