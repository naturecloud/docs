---
title: 常见问题
taxonomy:
    category: docs
---


1.Q:dockerfile里的from下载官方镜像慢

	A:可以先从naturecloud.io的官方镜像市场中，pull到本地，然后再进行docker build

2.Q:dockerfile里的添加依赖下载慢
	
	A:建议添加aliyun的源
	例如 unbuntu:trusty
	RUN echo "deb http://mirrors.aliyun.com/ubuntu/ trusty main restricted universe multiverse" > /etc/apt/sources.list
	RUN echo "deb http://mirrors.aliyun.com/ubuntu/ trusty-security main restricted universe multiverse" >> /etc/apt/sources.list
	RUN echo "deb http://mirrors.aliyun.com/ubuntu/ trusty-updates main restricted universe multiverse" >> /etc/apt/sources.list
	RUN echo "deb http://mirrors.aliyun.com/ubuntu/ trusty-proposed main restricted universe multiverse" >> /etc/apt/sources.list
	RUN echo "deb http://mirrors.aliyun.com/ubuntu/ trusty-backports main restricted universe multiverse" >> /etc/apt/sources.list
	RUN echo "deb-src http://mirrors.aliyun.com/ubuntu/ trusty main restricted universe multiverse" >> /etc/apt/sources.list
	RUN echo "deb-src http://mirrors.aliyun.com/ubuntu/ trusty-security main restricted universe multiverse" >> /etc/apt/sources.list
	RUN echo "deb-src http://mirrors.aliyun.com/ubuntu/ trusty-updates main restricted universe multiverse" >> /etc/apt/sources.list
	RUN echo "deb-src http://mirrors.aliyun.com/ubuntu/ trusty-proposed main restricted universe multiverse" >> /etc/apt/sources.list
	RUN echo "deb-src http://mirrors.aliyun.com/ubuntu/ trusty-backports main restricted universe multiverse" >> /etc/apt/sources.list

3.Q:dockerfile如何处理yes or no 交互?
	
	A: 在dockerfile里没有shell命令的交互，所以在安装的时候的需要 -y 默认yes。 
	   在碰到有些安装的时候需要用debconf-set-selections进行模拟确认来避开交互。
	   例如：
	   apt-get install -y  oracle-java7-installer
	   需要用下命令在安装前模拟
	   RUN echo oracle-java7-installer shared/accepted-oracle-license-v1-1 select true | debconf-set-selections
4.Q:在启动容器需要启动多个进程怎么办？
	
	A:



