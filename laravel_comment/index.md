启动的入口，位于public/index.php代码中。  

```php

$app = require_once __DIR__.'/../bootstrap/app.php';

//始初化的一个核心方法。
```

```php
$app = new Illuminate\Foundation\Application(
    //data/httpd/laravel
    realpath(__DIR__.'/../')
);
//这里直接文件作return了，奇怪的用法
```

```php
//new Illuminate\Foundation\Application的构造方法，具体做了什么事情？
public function __construct($basePath = null)
{
    //这个时候我的basePath是：/data/httpd/laravel
    if ($basePath) {//所以开始设置
        $this->setBasePath($basePath);
    }
    $this->registerBaseBindings();
    $this->registerBaseServiceProviders();
    $this->registerCoreContainerAliases();
}
```


```php
$kernel = $app->make(Illuminate\Contracts\Http\Kernel::class);
```

调用`$app`中的方法：  
```php

```
