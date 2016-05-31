---
title: Dockerfile例子
taxonomy:
    category: docs
---


    FROM naturecloud.io/library/nodejs:latest
    
    #Add files to the image
    
    RUN mkdir -p /opt/nodejs
    ADD . /opt/nodejs
    WORKDIR /opt/nodejs
    
    CMD node index.js
