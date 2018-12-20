Docker在build镜像的时候，如果某个命令相关的内容没有变化，会使用上一次缓存（cache）的文件层，在构建业务镜像的时候可以注意下面两点：



- 不变或者变化很少的体积较大的依赖库和经常修改的自有代码分开；
- 因为cache缓存在运行Docker build命令的本地机器上，建议固定使用某台机器来进行Docker build，以便利用cache。



下面是构建Spring Boot应用镜像的例子，用来说明如何分层。其他类型的应用，比如Java WAR包，Nodejs的npm模块等，可以采取类似的方式。



1、在Dockerfile所在目录，解压缩maven生成的jar包。



```
$ unzip <path-to-app-jar>.jar -d app
```

2、Dockerfile我们把应用的内容分成4个部分COPY到镜像里面：其中前面3个基本不变，第4个是经常变化的自有代码。最后一行是解压缩后，启动spring boot应用的方式。



```
FROM openjdk:8-jre-alpine

LABEL maintainer "xdmdpz@foxmail.com"
COPY app/BOOT-INF/lib/ /app/BOOT-INF/lib/
COPY app/org /app/org
COPY app/META-INF /app/META-INF
COPY app/BOOT-INF/classes /app/BOOT-INF/classes
EXPOSE 8080
CMD ["/usr/bin/java", "-cp", "/app", "org.springframework.boot.loader.JarLauncher"]
```

这样在构建镜像时候可大大提高构建速度。