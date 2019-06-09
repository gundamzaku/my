win下面报错：`vue SyntaxError: missing ) after argument list`  
启动项中把--hot去掉  

webpackJsonp is not defined  
这是因为公共文件必须在自己引用的js文件之前引用，可以手动改文件引用。  
找到build→webpack.prod.conf.js→找到HtmlWebpackPlugin插件，添加如下配置：  
chunks: ['manifest','vendor','admin']  

#Unexpected end of JSON input while parsing near '...ture":"-----BEGIN PGP
npm cache clean --force
