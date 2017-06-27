# 发展的历程
从 数据访问框架(ORM) -> Web框架(MVC) -> 分布式服务框架(RPC)  -> 资源调度和治理中心(SOA)
主要解决的是千万级用户量的处理。

### 安装mvn
http://maven.apache.org/download.cgi
在windows的环境变量中配置

在checkout出来的dubbox目录执行mvn install -Dmaven.test.skip=true来尝试编译一下dubbo（并将dubbo的jar安装到本地maven库）
似乎不用这么复杂，直接去MAVEN上下载即可？

```
服务提供者\服务消费者
```
## 服务提供者

## 基于Zookeeper的注册中心
