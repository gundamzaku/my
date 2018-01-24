1、超级变量  

$GLOBALS 	数组 	存放了所有的全局变量  
$_SERVER 	数组 	请求头信息以及服务器环境信息  
$_GET 	数组 	通过GET请求传递给服务器的键值对  
$_POST 	数组 	通过POST请求传递给服务器的键值对  
$_COOKIE 	数组 	COOKIE数组  
$_REQUEST 	数组 	包含所有$_GET、$_POST、$_COOKIE的数据  
$_SESSION 	数组 	SESSION数组  
$_FILES 	数组 	与文件上传相关的数组  
$_ENV 	数组 	环境变量数组  

2、客户端IP，服务端IP  

$ip = $_SERVER['REMOTE_ADDR'];  
$ip = getenv('HTTP_CLIENT_IP');  

$_SERVER['SERVER_ADDR'];

3、time  
方法一  
$day = date("Y")."-".date("m")."-".(date("d")-1).date(" H:i:s");  
方法二  
date("Y-m-d H:i:s",time()-86400);  
方法三  


4  
require一个文件存在错误的话，那么程序就会中断执行了，并显示致命错误  
include一个文件存在错误的话，那么程序不会中端，而是继续执行，并显示一个警告错误。  

require通常放在PHP程序的最前面  
include一般是放在流程控制的处理部分中PHP程序网页在读到include的文件时，才将它读进来。这种方式可以把程序执行时的流程简单化。  
php5以后，因为有autoload的机制，代码中的include已经少了。  

5  
filter_var($email, FILTER_VALIDATE_EMAIL));  
$rs = preg_match("/[a-zA-Z0-9\.\_\-]+\@[a-zA-Z0-9\.\_\-]+\.(com)|(cn)$/",$email);  

6  
实际代码中用eloquent插件实现orm代码  
```
$db = new PDO('mysql:host=localhost;dbname=spring', 'liudan', 'liudan123');
$stmt = $db->prepare("select * from Student where NAME=?");
$value = 'Zara';
$stmt->bindParam(1, $value, PDO::PARAM_STR, 256);
$stmt->execute();
while ($rs = $stmt->fetch(PDO::FETCH_ASSOC)){
  print_r($rs);
}
```

7、isset,empty()  

8、

9、
`
$fruit['fruit'][]['apple'] = '苹果';
$fruit['fruit'][]['banana'] = '香蕉';

$fruitDesc = json_encode($fruit);
echo "var testjson=".$fruitDesc.";";
`

10、  
默认机制，用磁盘文件来实现PHP会话。存入tmp目录中。client端用cookie存储对应的sessionid用于保持。
目前的话，大多会将Session写入内存中，在Php.ini中设置，写到memcache里面。  

session.save_path = "tcp://127.0.0.1:11211"  

session_start()
$_SESSION[]设置
session_destory()

11、  
```
E_WARNING  
E_ALL  
E_NOTICE  
error_reporting(E_ALL & ~E_NOTICE);   

display_errors = Off    
log_errors = On    
error_log = /var/log/cron/error.log  
error_reporting = E_ALL  
```

12、  

我可能会用Mq。
读写分离，读用来查询。写用来发送道具。  
分表，按日期来拆分，一天一个归档。  
一般来说游戏一个服不会有这么多数据，可能有多个服，也可以考虑按服来分表。  
索引  
用MYSQL写队列  
做好压力测试。  

13、C

14、  
6,4,4,4,4  

15、  
-rwxrwxrwx 1 root root 1393 jul 2 11:30 test  
drwxr-xr-x 2 edit users 4096 jun 23 17:26 pay  

```
d：表示为目录 l为link  
rwx：user拥有所有权限
r-x：group拥有read与execute权限，无wirte权限
r-x：other拥有read与execute权限，无wirte权限
12表示子目录  
用户，组，文件大小，修改日期，文件名  
```
