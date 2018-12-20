对 Linux 系统自身来说，影响 timezone 的是 /etc/localtime 这个文件，对于安装了 tzdata 包的系统，在 /usr/share/zoneinfo 目录下有各 timezone 的文件，以 'Asia/Shanghai' 为例指定 timezone 可以
`sudo ln -fs /usr/share/zoneinfo/Asia/Shanghai /etc/localtime`
也可以
`sudo cp /usr/share/zoneinfo/Asia/Shanghai /etc/localtime`
如果保留 tzdata 推荐 ln，否则就 cp。只要 /etc/localtime 是正确的文件，卸载掉 tzdata 当前 timezone 依然有效。

环境变量 TZ 可以覆盖系统的 timezone 设置，前提是 tzdata 存在，但是 Java 自带这些数据，没有 tzdata 时 TZ 照样生效。



#### Dockerfile 里设定 timezone

给 Java 等自带时区信息的程序使用只需要类似 `ENV TZ=Asia/Shanghai` 即可，需要整个容器设置或者程序没有自带时区的使用下面的方法。



##### Ubuntu 安装和指定 timezone

```
ENV TZ=Asia/Shanghai

RUN apt-get update \
 && apt-get install -y tzdata \
 && ln -fs /usr/share/zoneinfo/$TZ /etc/localtime \
 && rm -rf /var/lib/apt/lists/*
```

不用判断 tzdata 是否存在，直接更新到最新版本更好。



##### Alpine 安装和指定 timezone

```
RUN apk add --no-cache tzdata \
 && cp /usr/share/zoneinfo/Asia/Shanghai /etc/localtime \
 && apk del tzdata
```

注意上面2种方式分别使用了 ln / cp 的方式，并且一个设置了 TZ 一个没有，根据需要自由组合使用。