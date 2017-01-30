# Nginx 容器 Exit\(0\) 退出原因

一直使用 Docker Hub 的镜像部署，出于学习目的，自己制作 Nginx 镜像。

但使用 \`docker-compose up\` 部署运行时，一直提示 \`Exit\(0\)\`， 并退出容器。

经过查找资料，发现需要把 nginx 的守护进程模式关闭掉。

因为docker-compose 运行时， 运行 nginx 的时候，默认的是开启守护进程，直接放在后台执行。导致 docker-compose 无法检测到当前运行的东西是否还活着。

所以使用 docker-compose 部署 nginx 的容器，需要设置 **nginx.conf **配置文件里面的

```
daemon off
```

如果不设置则默认为 \`on\`。

也可以使用 \`nginx -g "daemon off;" \` 在运行时添加全局变量。

这样就可以在 docker-compose 脚本中添加这个参数，不用修改 nginx 的配置文件。

