参数说明： -n 请求数量， -c 并发数量  

-n在测试会话中所执行的请求个数。默认时，仅执行一个请求。  

-c一次产生的请求个数。默认是一次一个。  

-t测试所进行的最大秒数。其内部隐含值是-n 50000，它可以使对服务器的测试限制在一个固定的总时间以内。默认时，没有时间限制。  

-p包含了需要POST的数据的文件。  
-p postdata.json
```
{
  "className": "User",
  "methodName": "addUser",
  "paramSet": {
    "user_01": {
      "a1": ["张yi",1471337924226],
      "a2": "马山"
    },
    "user_02": "21",
    "user_03": "男"
  }
}
```

-T 设置请求头中的Content-type（针对POST/PUT），比如：application/x-www-form-urlencoded。默认是text/plain。
-T application/json

-w 将测试结果打印到HTML表格中。

ab -n1000 -c10 http://www.baidu.com/index.html  

**ab性能指标**

在进行性能测试过程中有几个指标比较重要：

`1、吞吐率（Requests per second）`

服务器并发处理能力的量化描述，单位是reqs/s，指的是在某个并发用户数下单位时间内处理的请求数。某个并发用户数下单位时间内能处理的最大请求数，称之为最大吞吐率。

记住：吞吐率是基于并发用户数的。这句话代表了两个含义：

a、吞吐率和并发用户数相关

b、不同的并发用户数下，吞吐率一般是不同的

计算公式：总请求数/处理完成这些请求数所花费的时间，即

Request per second=Complete requests/Time taken for tests

必须要说明的是，这个数值表示当前机器的整体性能，值越大越好。

`2、并发连接数（The number of concurrent connections）`

并发连接数指的是某个时刻服务器所接受的请求数目，简单的讲，就是一个会话。

`3、并发用户数（Concurrency Level）`

要注意区分这个概念和并发连接数之间的区别，一个用户可能同时会产生多个会话，也即连接数。在HTTP/1.1下，IE7支持两个并发连接，IE8支持6个并发连接，FireFox3支持4个并发连接，所以相应的，我们的并发用户数就得除以这个基数。

`4、用户平均请求等待时间（Time per request）`

计算公式：处理完成所有请求数所花费的时间/（总请求数/并发用户数），即：

Time per request=Time taken for tests/（Complete requests/Concurrency Level）

`5、服务器平均请求等待时间（Time per request:across all concurrent requests）`

计算公式：处理完成所有请求数所花费的时间/总请求数，即：

Time taken for/testsComplete requests

可以看到，它是吞吐率的倒数。

同时，它也等于用户平均请求等待时间/并发用户数，即

Time per request/Concurrency Level  

**常用：**  

`Concurrency Level`    
并发数多少，等于-c后面的数值

`Time taken for tests`  
测试总耗时

`Complete requests`  
成功收到返回的数目

`Failed requests`  
请求失败数目，可能因为网络连接，异常，请求数据长度等等

`Non-2xx responses`  
表示返回的HTTP status code不是2xx的数目（比如404,401,500...），如果都是2xx，这个指标不显示在结果里面

`Requests per second`  
每秒请求数，等于总请求数/测试总耗时

`Time per request`  
每一个请求平均花费时间。第一个Time per request等于concurrency * timetaken * 1000 / done，第二个Time per request（mean, across all concurrency requests）等于timetaken * 1000 / done，第一个可以理解为用户平均请求等待时间，第二可以理解为服务器平均请求等待时间
