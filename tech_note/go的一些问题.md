### 编译的问题  
在intellij下面，选go application时，package怎么填。  
src/main/source1.go source2.go  
然后paceage里填main，即可直接对main目录编译  


通过go get -v可以查看到安装package的详情

#go env 查看环境信息  

go被墙的处理方式：  
```
$mkdir -p $GOPATH/src/golang.org/x/
$cd $GOPATH/src/golang.org/x/
$git clone https://github.com/golang/net.git net 
$go install net
```
