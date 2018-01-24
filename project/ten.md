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
