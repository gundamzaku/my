# 发展的历程
从 数据访问框架(ORM) -> Web框架(MVC) -> 分布式服务框架(RPC)  -> 资源调度和治理中心(SOA)
主要解决的是千万级用户量的处理。

### 安装mvn
http://maven.apache.org/download.cgi
在windows的环境变量中配置

mvn install -Dmaven.test.skip=true来尝试编译一下项目（并将jar安装到本地maven库）
似乎不用这么复杂，直接去MAVEN上下载即可？

yum install automake libtool flex bison pkgconfig gcc-c++ boost-devel libevent-devel zlib-devel python-devel ruby-devel  
yum -y install openssl openssl-devel  

最后的安装是用`./configure --disable-tests --disable-tutorial`完成的

` ./bootstrap.sh`在下载的包里面没有，是于git库上clone下来的source里面copy过去再执行的，很奇怪
`./configure --with-boost-libdir=/usr/local/lib`之前用过这个命令，是因为boost默认的安装目录是在这里，而thrift编译的时候似乎是从lib64中去拿的。  
之前有报`libboost_unit_test_framework`的错误，是因为boost没装的关系，尽管yum里面显示已经装了，所以下载source重新自己装一次。
`./bootstrap.sh`->`./b2 install`  
大至上就这么多，另外记得需要有足够的内够，不然也会报错。  
参考网址：http://thrift.apache.org/docs/install/

```
服务提供者\服务消费者
```
## 服务提供者
