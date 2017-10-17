下载：
`http://php.net/get/php-7.1.10.tar.gz/from/a/mirror`  

```
$ cd ext/
$ ./ext_skel --extname=dan
$ Creating directory dan
```

创建扩展文件的源代码  

```
$ [root@6c6aa7fb57ef dan]# ls
$ CREDITS  EXPERIMENTAL  config.m4  config.w32  dan.c  dan.php  php_dan.h  tests
```

需要修改config.m4文件  

```
扩展的 config.m4 文件告诉 UNIX 构建系统哪些扩展 configure 选项是支持的，你需要哪些扩展库，以及哪些源文件要编译成它的一部分。
```

#dnl 为注释
```
dnl Comments in this file start with the string 'dnl'.
这个文件中是用'dnl'作为注释的。
dnl Remove where necessary. This file will not work
dnl without editing.
哪里需要移哪里。不这样这文件就不工作。

dnl If your extension references something external, use with:
如果你的扩展需要引用一些外部内容，用下面：
dnl PHP_ARG_WITH(dan, for dan support,
dnl Make sure that the comment is aligned:
dnl [  --with-dan             Include dan support])

dnl Otherwise use enable:
否则使用enable

dnl PHP_ARG_ENABLE(dan, whether to enable dan support,
dnl Make sure that the comment is aligned:
dnl [  --enable-dan           Enable dan support])
```
这个暂时不是特别能够理解。先随便去掉一个吧。  
```
PHP_ARG_WITH(dan, for dan support,
Make sure that the comment is aligned:
[  --with-dan             Include dan support])
```

```
./configure --with-php-config=./configure --with-php-config=/usr/bin/php-config
```

```
$ make && make install
$ make test
```

呃……这就编完了？代码在哪？  

```
Libraries have been installed in:
   /tmp/php-7.1.10/ext/dan/modules
```
