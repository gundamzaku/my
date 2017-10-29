## PHP_MINIT_FUNCTION(MyModule);

当模块被Zend Engine(ZE)加载后，例如Apache启动，加载了PHP模块，ZE会对每一个扩展模块调用此函数（如果有的话），可以在该函数里进行一些初始化操作。
