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
./configure --without-php --without-perl --without-ruby --without-haskell --without-go --without-d --without-csharp --without-erlang --without-c_glib
```
服务提供者\服务消费者
```
## 服务提供者
