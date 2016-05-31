---
title: 如何往镜像里添加文件
taxonomy:
    category: docs
---

	COPY <src>  <dest>
将文件<src\>拷贝到container的文件系统对应的路径<dest\>下。<src\>可以是文件、文件夹，对于文件和文件夹<src\>必须是在Dockerfile的相对路径下（build context path），即只能是相对路径且不能包含`../path/`。

<dest\>可以是容器中的绝对路径，也可以是当前`WORKDIR`指定的目录。
