### 查看密码  
```
mysql>use mysql;
mysql>select user, host, plugin, authentication_string from user\G;
***************** 2. row *****************
user: root
host: %
plugin: caching_sha2_password 
```
