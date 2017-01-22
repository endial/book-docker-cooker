# Docker daemon {#docker-daemon}

Docker daemon是Docker最核心的后台进程，它负责响应来自Docker client的请求，然后将这些请求翻译成系统调用完成容器管理操作。该进程会在后台启动一个API Server,负责接收由Docker client发送的请求；接收到的请求将通过Docker daemon内部的一个路由分发调度，再由具体的函数来执行请求。

