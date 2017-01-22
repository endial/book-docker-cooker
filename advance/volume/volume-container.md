# 数据卷容器

**约定**：

* datacenter-alpine：镜像名称
* datacenter： 创建后的容器名称
* host-dir：宿主机目录名
* data-dir：容器中卷名称

如果你有一些持续更新的数据需要在容器之间共享，最好创建数据卷容器。

数据卷容器，其实就是一个正常的容器，专门用来提供数据卷供其它容器挂载的。



## 数据卷创建

数据卷创建有多重方式：

* 创建不指定宿主机目录的数据卷容器：

```
~$ docker run -d -v /data-dir --name datacenter datacenter-alpine /bin/sh
```

* 挂载本地目录的数据卷容器，可以使用多个 `-v` 指定多个路径：

```
~$ docker run -d -v host-dir:/data-dir --name datacenter datacenter-alpine /bin/sh
~$ docker run -d -v host-dir:/data-dir -v host-dir1:/data-dir1 --name datacenter datacenter-alpine /bin/sh
```

* 挂载一个宿主机文件作为数据卷：

```
~$ docker run -it -v ~/.bash_history:/.bash_history --name datacenter datacenter-alpine /bin/sh
```



## 数据卷的使用

然后，在其他容器中使用 `--volumes-from` 来挂载 datacenter 容器中的数据卷。

```
~$ docker run -d --volumes-from datacenter --name db1 training/postgres
~$ docker run -d --volumes-from datacenter --name db2 training/postgres
```

还可以使用多个 `--volumes-from` 参数来从多个容器挂载多个数据卷。 也可以从其他已经挂载了数据卷的容器来挂载数据卷。

```
~$ docker run -d --name db3 --volumes-from db1 --volumes-from db2 training/postgres
```

> 注意：使用 `--volumes-from` 参数所挂载数据卷的容器自己并不需要保持在运行状态。

如果删除了挂载的容器（包括 datacenter、db1 和 db2），数据卷并不会被自动删除。如果要删除一个数据卷，必须在删除最后一个还挂载着它的容器时使用 `docker rm -v` 命令来指定同时删除关联的容器。 这可以让用户在容器之间升级和移动数据卷。