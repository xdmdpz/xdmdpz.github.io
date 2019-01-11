---
title: 使用docker部署前后端分离项目
date: 2019-01-02 13:40:40
tags: docker 
header-img: "img/header_img/archive-bg.png"
subtitle: "记录下思考过程"
---

最近项目快来发完了，就寻思弄一套部署方法

技术栈是这样的  
- 服务端 spring-boot 
- 前端 vue+webpack 
- 数据库 mysql       
- 图片服务器 zimg

然后准备用docker部署、数据库用阿里云的 

### 服务端方案
后端用的`alpine-glibc:glibc-2.27`+`openjdk`做基础镜像

**基础镜像Dockerfile**
```Dockerfile
FROM frolvlad/alpine-glibc:glibc-2.27

LABEL maintainer="xdmdpz <xdmdpz@gmail.com>"

ENV JDK_PACKAGE_NAME zulu8.31.0.1-jdk8.0.181-linux_x64.tar.gz
ENV JAVA_VERSION 8

ENV JAVA_PATH 512cd62ec5174c3487ac17c61aaa89e8
ENV JAVA_HOME /usr/local/jvm/default-jvm
ENV JAVA_DOWNLOAD_URL https://cdn.azul.com/zulu/bin/${JDK_PACKAGE_NAME}



RUN apk add --no-cache bash tar wget ca-certificates unzip \
    && mkdir -p ${JAVA_HOME} \
    && wget  ${JAVA_DOWNLOAD_URL} \
    && tar -xzf ${JDK_PACKAGE_NAME} -C ${JAVA_HOME} --strip-components=1 \
    && ln -s ${JAVA_HOME}/bin/* /usr/bin/ \
    && apk del tar wget ca-certificates unzip \
    && rm -rf   ${JDK_PACKAGE_NAME} \
                ${JAVA_HOME}/*src.zip \
                ${JAVA_HOME}/jre/lib/security/README.txt \
                /tmp/*

CMD ["bash"]
```
接着在基础镜像基础上加入项目jar包，并加入启动命令
**服务端Dockerfile**
```Dockerfile
FROM alpine-glibc-openjdk-8
VOLUME /tmp
ADD app.jar app.jar
ENV 8080
ENTRYPOINT ["java","-Djava.security.egd=file:/dev/./urandom","-Dspring.profiles.active=${SPRING_PROFILES_ACTIVE}","-Duser.timezone=GMT+08","-jar","/app.jar"]
```

### 前端方案

1. 开发时前端打包后，将编译后的项目用nginx启动。

    目录结构
    ```
    ├── dist/
    ├── nginx.conf
    └── Dockerfile
    ```
    Dockerfile
    ```Dockerfile
    FROM nginx
    COPY nginx.conf /etc/nginx/nginx.conf
    RUN mkdir /app
    WORKDIR /app
    COPY . /app/
    ENV PORT 80
    RUN mkdir -p /var/www/html/dist \
    &&  cp -r dist/* /var/www/html/dist \
    && rm -rf /app
    RUN echo "Asia/shanghai" > /etc/timezone
    ```
    获取nginx.conf的方法
    ```shell
     $ docker run --name tmp-nginx-container -d nginx
     $ docker cp tmp-nginx-container:/etc/nginx/nginx.conf ./nginx.conf 
     $ docker rm -f tmp-nginx-container
    ```

2. 后来觉得直接让前端打包成镜像就算了，写了一个在容器打包的方案

    Dockerfile
    ```Dockerfile
    FROM node:10.14.2-slim
    RUN apt-get update  && apt-get install -y nginx
    COPY nginx.conf /etc/nginx/nginx.conf
    RUN mkdir /app
    WORKDIR /app
    COPY . /app/
    ENV PORT 80RUN mkdir /var/www/html/dist \
        && npm install \
        && npm run build \
        && cp -r dist/* /var/www/html/dist \
        && cp -r index.html /var/www/html \
        && rm -rf /app
    RUN echo "Asia/shanghai" > /etc/timezoneCMD ["nginx","-g","daemon off;"]

    ```
    获取nginx.conf方法与上一个一样


---

后来觉得根据spring-boot的启动方式

前后端完全可以部署在一起，这样也省的每次前端打包都要改ip了

然后在查资料的过程中发现了一个Docker在构建项目上的一个特性

> 指定按照从上到下，顺序执行

> 每条指令都会创建一个新的镜像层，并对镜像进行提交

> 如果某个命令相关的内容没有变化，会使用上一次缓存（cache）的文件层

这个思路完全可行

下面演示下例子：

思路:
1. 使用jenkins检测指定分支代码更新

2. 使用打包工具打包并用时间戳命名（.jar、.zip）

3. 创建软连接后端代码 (LTS.jar) or 前端代码(LTS.zip)并解压
    - `ln -s -f 1547196831460.jar /LTS/LTS.jar`
    - `ln -s -f 1547196831460.zip /LTS/LTS.zip`
    
4. 构建image
    - 解压前后端项目
        - `rm -rf /LTS/java && unzip LTS.jar -d java` 
        - `rm -rf /LTS/vue && unzip LTS.zip -d vue`
    - Dockerfile
    ```Dockerfile
    FROM alpine-glibc-openjdk-8

    LABEL maintainer "xdmdpz@foxmail.com"

    COPY /LTS/java/BOOT-INF/lib/ /app/BOOT-INF/lib/
    COPY /LTS/java/org /app/org
    COPY /LTS/java/META-INF /app/META-INF
    COPY /LTS/java/BOOT-INF/classes /app/BOOT-INF/classes

    COPY /LTS/vue/* /app/BOOT-INF/classes

    EXPOSE 8080
    CMD ["/usr/bin/java", "-cp", "/app", "org.springframework.boot.loader.JarLauncher"]
    ```
5. 完事


Dockerfile我们把应用的内容分成5个部分COPY到镜像里面：

其中前面3个基本不变，

第4个是经常变化的后端代码，

第5个是打包后的前端代码。

最后一行是解压缩后，启动spring boot应用的方式。


这样在构建镜像时候可大大提高构建速度。


部署的时候注意一下两点：

- 不变或者变化很少的体积较大的依赖库和经常修改的自有代码分开
- 因为cache缓存在运行Docker build命令的本地机器上，建议固定使用某台机器来进行Docker build，以便利用cache。

以上是构建Spring Boot应用镜像，其他类型的应用，比如Java WAR包，Nodejs的npm模块等，可以采取类似的方式。



