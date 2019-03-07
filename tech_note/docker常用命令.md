#### 启动docker服务
service docker start  

#### 查看进程  
docker ps  
docker ps -a    

#### 删除镜像  
docker rmi f5bcc57eac41  

#### 进入  
docker attach 1eea2777d400

下面这个也能用  
docker exec -it web bash

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
docker run -d -i -t --name=mysql -P  database  

`名字&映射&端口`  
docker run -d -i -t --name=liwugame -P --link=mysql:db -p 8080:8080  php56  

`映射到另外一台主机`  
docker run -d -i -t --name=web -P --link=mysql:db -p 80:80  web  
`多个端口`
docker run -d -p 80:80 -p 22:22

`带端口`  
docker run -d -i -t -p8080:8080 centos  

#### 新用法  
**原来的--link已经不推荐了，用桥的方式**  
docker network create -d bridge tantanwen  
docker run -d -i -t --net tantanwen --name=web  --privileged=true -p 80:80 web  
后者是指images的  

docker run -d -i -t --net tantanwen --name=mysql --privileged=true -p 3306:3306 database  
两个容器加入到桥里面，可以ping，记得改一下Host，写进去的似乎默认是ImagesID  

#### 停止  
docker stop d65c25cf644f

#### 提交到镜像
docker commit 90639128ba28 php56

#### 查看镜像  
docker images

#### 如何退出容器而不停止容器？  

组合键：Ctrl+P+Q

#### 挂载目录  
docker run -d -i -t -v /source_php:/data/www --net tantanwen --name=wanda --privileged=true -p 80:80 -p 2181:2181 wanda  
注意，虚拟机的话是映射虚拟机的目录的。  

#### 启动MySQL  
docker run --name mysql5 -v /data/mysql5/datadir:/var/lib/mysql --net tantanwen -e MYSQL_ROOT_PASSWORD=dan2001go --privileged=true -p 3306:3306 -d mysql:5

docker run --name mysql8 -v /data/mysql/datadir:/var/lib/mysql --net tantanwen -e MYSQL_ROOT_PASSWORD=dan2001go --privileged=true -p 3306:3306 -d mysql:8

docker run --name mysql8 -v /mysql/datadir:/var/lib/mysql -v /mysql/conf.d:/etc/mysql/conf.d --net tantanwen -e MYSQL_ROOT_PASSWORD=dan2001go --privileged=true -p 3306:3306 -d mysql:8

docker run -d -i -t --net tantanwen --name=php --privileged=true -p 9000:9000 php

docker run --name nginx -v /data/dockerdata/web:/usr/share/nginx/html -v /data/dockerdata/nginx/conf.d:/etc/nginx/nginx.conf:ro --net tantanwen --privileged=true -p 80:80 -d nginx

 docker run -it --name php --net tantanwen -v /data/dockerdata/php:/data/ -p 9000:9000 --privileged=true centos

#### 查看日志
docker logs -f -t --tail 100 e79464636bca 
