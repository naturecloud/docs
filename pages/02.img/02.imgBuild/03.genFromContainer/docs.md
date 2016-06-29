---
title: 容器生成镜像
taxonomy:
    category: docs
---

容器生成镜像虽然并不推荐，但是对于那些不熟悉dockerfile的用户降低了门槛。

### 搭建Docker环境
搭建docker环境，不清楚的同学可以参考
[docker 安装](../../../q&a/docker-q&a)

### 拉取基础镜像
可以通过docker pull去官方或者naturecloud.io的镜像市场拉取自己所需操作系统基础镜像到本地仓库。

	docker pull naturecloud.io/ubuntu:trusty

然后再本地仓库里就可以看到

	root@node:~# docker images| grep  naturecloud.io/ubuntu
	naturecloud.io/ubuntu       trusty       2d24f826cb16        16 months ago       188.3 MB

将基础镜像docker run,然后进入镜像进行安装自己的环境依赖

	root@AY131229124202040c09Z:~# docker run -it naturecloud.io/ubuntu:trusty /bin/bash

	#下面就表示进入了容器
	root@e72d0f78365f:/# 

然后我们在容器里安装vim
	
	root@e72d0f78365f:/# apt-get install vim
	... ...
	root@e72d0f78365f:/# which vim
	/usr/bin/vim

然后退出容器后，找到刚刚创建的容器id
	
	docker ps -a | grep naturecloud.io/ubuntu:trusty
	e72d0f78365f        naturecloud.io/ubuntu:trusty                                      "/bin/bash"              51 minutes ago      Exited (130) 55 seconds ago                                                    cranky_feynman
	a793d87dbc14        naturecloud.io/ubuntu:trusty                                      "/bin/bahs"              51 minutes ago      Created     

将容器生成新的镜像

	root@node:~# docker commit e72d0f78365f test-images
	c868d49c60726e42172465234a84232a4ec3f87a14f24aeb9be4c790a9cfaae7
	root@node:~# docker images| grep test-image
	test-image    latest          c868d49c6072        13 seconds ago      191.4 MB
	         
将新创建的镜像run起来

	root@node:~# docker run -it c868d49c6072 /bin/bash
	root@2a20cf975d1c:/# which vim
	/usr/bin/vim

这个时候容器里就有我们之前安装过的命令了。

根据此方法我们可以搭建所需要的运行环境作为自己依赖的基础镜像，在这个基础上，将自己的可执行程序和启动脚本打入最终的镜像。
	
	#from之前制作的含环境依赖的基础镜像
	FROM test-image

	#添加可执行程序和脚本
	ADD xxx   /bin
	ADD run.sh  /
	
	#启动命令
	CMD [/run.sh]	


最后这个dockerfile build后，将它push到平台，上传具体可以参考[镜像上传](../generateImage#-1)

	
	
