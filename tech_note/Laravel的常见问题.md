运行时报错：  
The only supported ciphers are AES-128-CBC and AES-256-CBC with the correct key lengths.  

执行命令：php artisan key:generate  即可  

访问的报404：  
nginx里面加上
```
server
{
    root  /data/httpd/laravel/public;

    location / {
        try_files $uri $uri/ /index.php?$query_string;
    }  
}
```
