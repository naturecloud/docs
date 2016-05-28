---
title: 指定工作目录
taxonomy:
    category: docs
---

`WORKDIR`指令用于设置Dockerfile中的`RUN`、`CMD`指令执行命令的工作目录(默认为/目录)，该指令在Dockerfile文件中可以出现多次，如果使用相对路径则为相对于`WORKDIR`上一次的值。


例如

> `WORKDIR /a`，`WORKDIR b`，`RUN pwd`最终输出的当前目录是/a/b。
> 



