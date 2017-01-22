# Docker Client {#docker-client}

Docker client是一个泛称,用来向指定的Docker daemon发起请求,执行相应的容器管理操作.它既可以是Docker命令行工具，也可以是任何遵循了Docker API的客户端.目前, 社区中维护着的Docker clien种类非常丰富,涵盖了包括C\#\(支持 Windows\)、Java、Go、Ruby、JavaScript等常用语言，甚至还有使用Angular库编写的WebU格式的客户端，足以满足大多数用户的需求。

在Linux系统下,Docker Client 和Docker daemon和容器直接运行在宿主机上，这意味着容器可直接使用宿主机端口资源，不需要在容器和宿主机之间映射端口。

![](/imgs/linux_docker_host.svg)

在Windows或Max X系统下, Docker daemon运行在Linux虚拟机里，Docker client运行宿主机下window下跟Docker daemon对话。 当运行容器里，它用的端口资源是虚拟机里的，必须跟宿主机上的端口映射。

![](/imgs/win_docker_host.svg)

