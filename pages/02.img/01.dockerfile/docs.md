---
title: Dockerfile 
taxonomy:
    category: docs
---

Dockerfile对应创建镜像的过程，包含了创建镜像的指定序列。

下面是一个Dockerfile的样例

	FROM registry.naturecloud.io/hjqi/java:1.7         
	#以java为基础镜像  
	#registry.naturecloud.io 是镜像仓库
	#hjqi/java   是镜像
	#1.7  是引用镜像的版本
	
	ADD . /usr/src/myapp
	#将和dockerfile同级目录的所有文件拷贝到容器里的目标地址/usr/src/myapp
	#例如tomcat，常常会把war包放到tomcat的home目录的webapps下
	#ADD xx.war   /tomcat/webapps

	WORKDIR /usr/src/myapp
	#设置容器的工作目录，进入容器后显示的当前目录
	#程序里需要用到的工作目录，可以用WORKDIR来设置

	RUN javac Main.java
	#执行shell命令

	CMD ["java", "Main"]
	#容器的启动命令

---

    FROM 115.28.226.88:5000/hjqi/node:latest   #以nodejs为基础镜像
    
    #Add files to the image
    
    RUN mkdir -p /opt/nodejs                    #创建目录/opt/nodejs
    ADD . /opt/nodejs                           #将当前目录的内容复制到/opt/nodejs
    WORKDIR /opt/nodejs                         #将/opt/nodejs指定为工作目录
    
    CMD node index.js                           #镜像启动时需要命令"node index.js"

Dockerfile支持支持的语法命令为INSTRUCTION argument。指令不区分大小写。但是，命名约定为全部大写。下面介绍几个常用的Dockerfile指令

### 如何配置基础环境 ###

语法： `FROM <image>:<tag>`

在Dockerfile中第一条非注释INSTRUCTION一定是FROM，它决定了以哪一个镜像作为基准。`<image>`表示镜像名称，tag表示所选的tag（版本号）。

例子:

	FROM 115.28.226.88:5000/hjqi/nginx:1.9.14 
  
以naturecloud上的版本号为1.9.14的nginx镜像为基础镜像


!! 如果Dockerfile中选的基础镜像来自自然云的官方镜像，请采用如下格式115.28.226.88:5000/hjqi/nginx:1.9.14

### 如何安装软件 ###


`RUN <commnad>`

例子：
>在ubuntu环境中安装vim
>
```
    RUN apt-get install vim
```

### 执行Shell命令 ###


`RUN <commnad>`

例子：
>创建目录/data/log
>
```
RUN mkdir –p /data/log
```

### 指定工作目录 ###


`WORKDIR`指令用于设置Dockerfile中的`RUN`、`CMD`指令执行命令的工作目录(默认为/目录)，该指令在Dockerfile文件中可以出现多次，如果使用相对路径则为相对于`WORKDIR`上一次的值。


例如

> `WORKDIR /a`
> `WORKDIR b`

最终的工作目录是/a/b。

### 如何往镜像里添加文件 ###

	COPY <src>  <dest>

例如

> `COPY src /src`

将同级的src目录，拷贝到容器里根目录下的src目录


将文件<src\>拷贝到container的文件系统对应的路径<dest\>下。<src\>可以是文件、文件夹。

<dest\>可以是容器中的绝对路径，也可以是当前`WORKDIR`指定的目录。


!!对于文件和文件夹<src\>必须是在Dockerfile的相对路径下（build context path），即只能是相对路径且不能包含`../path/`。



### 设置环境变量 ###

    ENV <key> <value>

例如

> `ENV JAVA_HOME /root/java/jdk1.7.0_51`

设置容器里的java_home是容器里的/root/java/jdk1.7.0_51目录

.. note::
	设置了后，后续的`RUN`命令都可以使用，当运行生成的镜像时这些环境变量依然有效

### 容器启动时运行的命令 ###

    CMD command param1 param2
例如：

> nginx启动时要运行命令`nginx -g daemon off`，则
> 
```
CMD nginx -g daemon off
```

Dockerfile更详细的用法请参考

[http://seanlook.com/2014/11/17/dockerfile-introduction/](http://seanlook.com/2014/11/17/dockerfile-introduction/)

[https://docs.docker.com/engine/reference/builder/](https://docs.docker.com/engine/reference/builder/)