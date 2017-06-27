#### 删除镜像  
docker rmi f5bcc57eac41  

#### 进入  
docker attach 1eea2777d400

#### 启动  
docker run -d -i -t --name=web -P --link=mysql:db -p 80:80  web

#### 删除  
docker rm 9e643d5cb23d

#### 开始  
docker start 9e643d5cb23d

#### 启动的几个参数  
`带端口`  
docker run -d -i -t --privileged=true -p 80:80 web  
`带端口，这是数据库的`  
docker run -d -i -t --privileged=true -p 3306:3306 database  
`带名字`  
docker run -d -i -t --name=mysql -P  database  ·
`名字&映射&端口`  
docker run -d -i -t --name=liwugame -P --link=mysql:db -p 8080:8080  php56  
`映射到另外一台主机`  
docker run -d -i -t --name=web -P --link=mysql:db -p 80:80  web  
`带端口`  
docker run -d -i -t -p8080:8080 centos  

#### 停止  
docker stop d65c25cf644f

#### 提交到镜像
docker commit 90639128ba28 php56

#### 查看镜像  
docker images

#### 如何退出容器而不停止容器？  

组合键：Ctrl+P+Q
