
### 资料
[Docker 中文指南](http://www.widuu.com/chinese_docker/index.html)
http://www.docker.org.cn/book/docker/prepare-docker-5.html


### 安装docker
```
#安装
 yum -y install docker-io
    #No package docker available yum没有找到docker包，更新epel第三方软件库
    sudo yum install epel-release

    yum install cgroup-lite

#启动 Docker 后台服务
service docker start

#默认开机启动
chkconfig docker on

#本地没有hello-world这个镜像，所以会下载一个hello-world的镜像，并在容器内运行
docker run hello-world

###运行镜像  以 ubuntu15.10 镜像创建一个新容器
#ubuntu:15.10指定要运行的镜像，Docker首先从本地主机上查找镜像是否存在，如果不存在，Docker 就会从镜像仓库 Docker Hub 下载公共镜像。
#/bin/echo "Hello world": 在启动的容器里执行的命令
docker run ubuntu:15.10 /bin/echo "Hello world"

#-t:在新容器内指定一个伪终端或终端。
#-i:允许你对容器内的标准输入 (STDIN) 进行交互。
 -d：以进程方式运行的容器 后台模式
 -p 标识来绑定指定端口  -p 5000:5000   指定容器端口绑定到主机端口
 -P 将容器内部使用的网络端口映射到我们使用的主机上  容器内部端口随机映射到主机端口
 --name 命名容器
docker run -i -t ubuntu:15.10 /bin/bash


#容器连接  --link name:alias  alias是link的别名
docker run -d -P --name web --link db:db training/webapp python app.py


#登录docker hub
docker login




#在容器内部创建一个新的卷/webapp
docker run -d -P --name web -v /webapp training/webapp python app.py

#挂载本地主机目录/src/webapp到容器中  添加了ro选项来限制它只读
docker run -d -P --name web -v /src/webapp:/opt/webapp[:ro] training/webapp python app.py


#将宿主机的一个特定文件挂载为数据卷  会在容器中运行一个bash shell，当你退出此容器时在主机上也能够看到容器中bash的命令历史
docker run --rm -it -v ~/.bash_history:/.bash_history ubuntu /bin/bash


#创建一个指定名称的数据卷容器
docker run -d -v /dbdata --name dbdata training/postgres echo Data-only container for postgres
#在另外一个容器使用--volumes-from标识，通过刚刚创建的数据卷容器来挂载对应的数据卷
docker run -d --volumes-from dbdata --name db1 training/postgres
















```



### 常用命令
```
#查看所有正在运行中的容器列表  inspect查看更详细信息
docker ps
docker inspect 容器id

#获得容器的id
docker ps -l

#查看容器内的标准输出
# -f 像使用tail -f 一样来输出容器内部的标准输出
docker logs [-f] 698

#可以查看指定 （ID或者名字）容器的某个确定端口映射到宿主机的端口号
docker port 698

#查看容器内部运行的进程
docker top 698

#保存对容器的修改，（698容器的ID-通过docker ps -l 命令获得）并把这个镜像保存为learn/ping
docker commit 698 learn/ping

#停止容器
docker stop 698

#启动应用容器
docker start 698

#移除应用容器 删除容器时，容器必须是停止状态
docker rm 698


#列出本地主机上的镜像
docker images

#使用版本为15.10的ubuntu系统镜像来运行容器(如果你不指定一个镜像的版本标签, 将默认使用 ubuntu:latest 镜像)
 使用镜像来创建一个容器
 在运行的容器内使用 apt-get update 命令进行更新。
 在完成操作之后，输入 exit命令来退出这个容器。
docker run -t -i ubuntu:15.10 /bin/bash




#构建一个镜像
    -t ：指定要创建的目标镜像名  标签6.7
    . ：Dockerfile 文件所在目录，可以指定Dockerfile 的绝对路径
docker build  -t youj/centos:6.7 .

#设置镜像标签dev
docker tag 860c279d2fec youj/centos:dev





#获取一个新的镜像
docker pull ubuntu:13.10

#查找镜像
docker search httpd

#拉取镜像
docker pull httpd

#使用镜像
docker run httpd


#创建一个容器
docker run -t -i ubuntu:15.10 /bin/bash

#提交容器副本
 -m:提交的描述信息
 -a:指定镜像作者
 e218edb10161：容器ID
 w3cschool/ubuntu:v2:指定要创建的目标镜像名 w3cschool/ubuntu:v2
docker commit -m="has update" -a="youj" e218edb10161 w3cschool/ubuntu:v2



#发布docker镜像到官方网站 只能将镜像发布到自己的空间下面
docker push


#删除你主机上的镜像不需要使用的容器
docker rmi training/sinatra








#运行容器
    -p 3306:3306：将容器的3306端口映射到主机的3306端口
    -v $PWD/conf/my.cnf:/etc/mysql/my.cnf：将主机当前目录下的conf/my.cnf挂载到容器的/etc/mysql/my.cnf
    -v $PWD/logs:/logs：将主机当前目录下的logs目录挂载到容器的/logs
    -v $PWD/data:/mysql_data：将主机当前目录下的data目录挂载到容器的/mysql_data
    -e MYSQL_ROOT_PASSWORD=123456：初始化root用户的密码
docker run -p 3306:3306
    --name mymysql
    -v $PWD/conf/my.cnf:/etc/mysql/my.cnf
    -v $PWD/logs:/logs
    -v $PWD/data:/mysql_data
    -e MYSQL_ROOT_PASSWORD=123456
    -d mysql:5.7

```


###构建镜像 docker build   创建一个 Dockerfile 文件



