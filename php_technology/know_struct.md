## PHP_MINIT_FUNCTION(MyModule);
当模块被Zend Engine(ZE)加载后，例如Apache启动，加载了PHP模块，ZE会对每一个扩展模块调用此函数（如果有的话），可以在该函数里进行一些初始化操作。

## PHP_RINIT_FUNCTION(MyModule);
对于每一个“使用”该模块的PHP脚本请求前，都执行该函数（如果有的话），最好的例子：Session扩展模块，如果在一个PHP脚本里执行session.start()，Session模块的PHP_RINIT_FUNCTION()将被调用。详情可以看看session模块的源代码。

## PHP_RSHUTDOWN_FUNCTION(MyModule);
与PHP_RINIT_FUNCTION()相反，该函数是在一个PHP脚本执行完毕后执行。

## PHP_MSHUTDOWN_FUNCTION(MyModule);
当ZE收到shutdown信号后，例如apache卸载PHP模块，ZE对每一个模块调用此函数，最后关闭自己的核心子系统。
