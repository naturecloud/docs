---
title: 5分钟入门
taxonomy:
    category: docs
---

下面通过hello world的例子，介绍如何使用平台进行应用的快速交付。

### 第一步：准备Dockerfile ###

<!--
- #### 直接写Dockerfile ####
-->

这个例子只有一个源码文件helloworld.html，helloworld.html放在跟Dockerfile同一个目录中。

	root@node:/data01/sample# ls
	Dockerfile  helloworld.html

Dockerfile内容如下
	
	FROM naturecloud.io/library/nginx:1.9.14
	ADD helloword.html /usr/share/nginx/html #将helloword.html添加到镜像中的目录/usr/share/nginx/html
    
helloworld.html内容如下
    
    <html>
        <head>
            <title>dockerfile test</title>
        </head>
        <body bgcolor="white" text="black">
            <center><h1>helloworld</h1></center>
        </body>
    </html>


<!--
- #### 通过容器完成Dockerfile过程 ####

	docker run 系统镜像，然后进入容器里安装依赖
	
		root@node:~# docker run  -it naturecloud.io/library/nginx:1.9.14 /bin/bash
		root@e72d0f78365f:~#apt-get install xxxx
		root@e72d0f78365f:exit
		root@node:~# docker ps -a | grep naturecloud.io/nginx:1.9.14
		e72d0f78365f        naturecloud.io/nginx:1.9.14                                      "/bin/bash"          51 minutes ago      Exited (130) 55 seconds ago     
		root@node:~# docker commit e72d0f78365f nginx-image
		c868d49c60726e42172465234a84232a4ec3f87a14f24aeb9be4c790a9cfaae7

	跟环境相关的依赖什么安装后，然后只需要将自己的最终的dockerfile from 之前的基础镜像，加入自己的执行程序和启动脚本即可。 
-->


### 第二步：生成镜像 ###

镜像是应用最终的交付件，选择以下两种的任一种生成镜像

- #### 方式一：平台构建 ####
	
	平台构建建可以对接github,bitbucket源码托管的平台。
    
    ##### 提交代码 #####

    将第一步中的Dockerfile和helloworld.html提交到github或者bitbucket. 假定项目名称为naturecloud-sample。
    
    ##### 创建构建 #####
    
    下面以bitbucket为例，介绍如何创建构建。

	![](buildcreate.png)

	![](sourcebuild.png)

	页面跳转到源码托管认证界面

	![](oauth-login.png)

	![](oauth-access.png)

	![](build-select.png)

	![](buildselect-1.png)

    ##### 执行构建 #####
    
	![](buildstart.png)

	![](buildstart-1.png)

	在构建列表里点击构建名称进入构建任务列表

	![](buildretlist.png)

	点击任务序号进入查看构建结果

	![](buildret.png)

	构建完成后可以在我的镜像中查看到之前构建的镜像

	![](myImage.png)
	
    后面当有新的代码版本时，只需找执行相应版本的构建即可。

- #### 方式二：线下构建 ####

    线下构建需要有一个docker环境。关于如何搭建docker环境，不清楚的同学可以参考[docker 安装](../../../q&a/docker-q&a)
	
	进入Dockerfile和helloworld.html所在目录

        root@node:/data01/sample# ls
	    Dockerfile  helloworld.html

    构建镜像

        root@node:/data01/sample# docker build -t nginx-image .
	
    给镜像打tag，将镜像推送到平台的registry

	    docker tag $IAMGE_ID   naturecloud.io/$namespace/$IAMGE_NAME # $IAMGE_ID是上一步的镜像id，$namespace是在平台的用户名，$IAMGE_NAME是镜像名
	    docker push naturecloud.io/$namespace/$IAMGE_NAME
		
	这时就可以在平台中，我的镜像里看到，之前push过来的镜像

### 第三步： 创建服务 ###

先选择之前上传的镜像，然后点击部署	

![](servicecreate-selectimage.png)

然后再服务创建信息页面填写相关参数

![](servicecreate-info.png)

最后点击创建，服务列表里可以看到之前创建的服务

![](servicelist.png)

### 第四步： 管理服务 ###



#### 服务详情 ####

点击服务名，进入服务详情页面

![](servicedetail.png)

**访问服务**

![](serviceAccess.png)

然后使用url，访问之前添加到helloworld.html

![](helloworld-test.png)

**查看日志**

![](servicedetail-log.png)

**登录服务**

![](servicedetail-console.png)

#### 版本更新 ####

在服务列表里面点击版本变更

![](serviceUpdate.png)

#### 启动/停止服务 ####

![](servicestartstop.png)

#### 伸缩 ####

通过伸缩扩容来增加/减少实例数目

![](servicescale.png)

#### 修改服务 ####

在服务列表里点击修改服务按钮，然后会进入和服务创建的相同的页面，进行服务信息的修改
![](serviceModify.png)

#### 删除服务 ####

点击服务列表里的删除按钮

![](servicedelete.png)

### 温馨提示 ###

通过5分钟入门，期望大家可以对自然云的使用有个基本的了解。要了解详细的内容，请参阅

1. 后续章节中对每一功能的详细介绍
2. [常见问题](../q&a)
