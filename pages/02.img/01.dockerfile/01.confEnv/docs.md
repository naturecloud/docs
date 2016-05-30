---
title: 如何配置基础环境
taxonomy:
    category: docs
---

语法： `FROM <image>:<tag>`

在Dockerfile中第一条非注释INSTRUCTION一定是FROM，它决定了以哪一个镜像作为基准。`<image>`表示镜像名称，tag表示所选的tag（版本号）。

例子:

	FROM 115.28.226.88:5000/hjqi/nginx:1.9.14 
  
以naturecloud上的版本号为1.9.14的nginx镜像为基础镜像


!! 如果Dockerfile中选的基础镜像来自自然云的官方镜像，请采用如下格式115.28.226.88:5000/hjqi/nginx:1.9.14
