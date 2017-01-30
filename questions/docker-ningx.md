# Nginx 容器 Exit\(0\) 退出原因

一直使用marathon部署docker的nginx镜像,

处于好奇,自己制作一个镜像,但是使用marathon部署自己制作的nginx镜像,一直无法成功,

使用 \`docker ps -a\` 查看,发现全是Exit\(0\) 

经过翻阅华为研发团队出版的docker书.

里面提到了,需要把nginx的守护进程模式关闭掉. 

因为marathon部署docker的时候,运行nginx的时候,默认的是开启守护进程,直接放在后台执行.导致marathon无法检测到当前运行的东西是否还活着.

所以使用marathon部署nginx的容器,需要设置**nginx.conf**配置文件里面的

```
daemon off
```

如果不设置则默认为on

&lt;&lt;深入理解nginx&gt;&gt;第二版 中提到,可以使用 nginx -g "deamon off" 来添加全局变量.

这样就可以在marathon脚本中添加这个参数,不用修改nginx的配置文件.

