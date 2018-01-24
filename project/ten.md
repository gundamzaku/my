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
$Link = new PDO('mssql:host=sqlserver;dbname=database', 'username','password');
