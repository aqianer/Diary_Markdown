引入Docker的背景:

1.程序员在不同环境的做同样的事执行的命令可能会不同,例如安装一个文本编辑器vim在ubuntu和centos的命令是不同的,

那如果是要把同一套代码部署到不同操作系统的服务器上呢?依赖的jar包还有配置文件就够头疼的了

2.这个程序在我的电脑跑的好好的,代码拉到你电脑跑不起来,为了让程序顺利跑起来就需要重新配置

> 依赖库+配置+操作系统=环境

为了让程序能在不同环境间顺利运行起来?引入了容器的概念



基础镜像:base image

> 用户空间+文件系统+依赖库

dockerfile

> 类似于脚本,将部署应用要做的事情都列出来然后用`docker build`命令构建程序所需要的环境 最后打包成压缩包称之为 Container Image

> `dockerfile + docker build = container image`

``` shell
docker build --压缩
docker push
docker pull
docker run  --解压缩
```



容器镜像可以采用Git仓库的方式进行管理

> 官方的Docker Hub , 非官方的Tuna(清华大学的镜像仓库)

docker的架构

docker&虚拟机





