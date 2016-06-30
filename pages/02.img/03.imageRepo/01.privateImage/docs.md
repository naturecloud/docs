---
title: 我的镜像
taxonomy:
    category: docs
---

我的镜像是用户的私有镜像，其来源有

- [代码构建](../../imgBuild/sourceBuild)。代码构建完成一次构建任务之后，自动会将生成的镜像推送到“我的镜像”仓库。
- [本地生成镜像](../../imgBuild/generateImage) 。本地通过dockerfile构建镜像。
- [容器生成镜像](../../imgBuild/genFromContainer)。基于某个基础镜像启动一个容器，在容器当中安装需要的环境，最后导出镜像。