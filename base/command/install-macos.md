## macOS 操作系统安装 Docker {#macos-操作系统安装-docker}

### 系统要求 {#系统要求}

[Docker for Mac](https://docs.docker.com/docker-for-mac/)要求系统最低为 macOS 10.10.3 Yosemite，或者 2010 年以后的 Mac 机型，准确说是带[Intel MMU 虚拟化](https://en.wikipedia.org/wiki/X86_virtualization#Intel-VT-d)的，最低 4GB 内存。如果系统不满足需求，可以考虑安装[Docker Toolbox](https://docs.docker.com/toolbox/overview/)。如果机器安装了[VirtualBox](https://www.virtualbox.org/)的话，VirtualBox 的版本不要低于 4.3.30。

### 安装 {#安装}

#### 使用 Homebrew 安装 {#使用-homebrew-安装}

[Homebrew](http://brew.sh/)的[Cask](https://caskroom.github.io/)已经支持 Docker for Mac，因此可以很方便的使用 Homebrew Cask 来进行安装：

```
brew cask install docker

```

#### 手动下载安装 {#手动下载安装}

如果需要手动下载，可以通过这个链接下载：[https://download.docker.com/mac/stable/Docker.dmg](https://download.docker.com/mac/stable/Docker.dmg)

如同 macOS 其它软件一样，安装也非常简单，双击下载的`.dmg`文件，然后将那只叫[Moby](https://blog.docker.com/2013/10/call-me-moby-dock/)的鲸鱼图标拖拽到`Application`文件夹即可（其间可能会询问系统密码）。

![](/imgs/install-mac-dmg.png)

### 运行 {#运行}

从应用中找到 Docker 图标并点击运行。



运行之后，会在右上角菜单栏看到多了一个鲸鱼图标，这个图标表明了 Docker 的运行状态。

![](/imgs/install-mac-menubar.png)

第一次点击图标，可能会看到这个安装成功的界面，点击 "Got it!" 可以关闭这个窗口。

![](/imgs/install-mac-success.png)

以后每次点击鲸鱼图标会弹出操作菜单。

![](/imgs/install-mac-menu.png)

_在国内使用 Docker 的话，需要配置加速器，在菜单中点击`Preferences...`，然后查看`Advanced`标签，在其中的`Registry mirrors`部分里可以点击加号来添加加速器地址。_

![](/imgs/install-mac-preference-advanced.png)

启动终端后，通过命令可以检查安装后的 Docker 版本。

```
$ docker --version
Docker version 1.12.3, build 6b644ec
$ docker-compose --version
docker-compose version 1.8.1, build 878cff1
$ docker-machine --version
docker-machine version 0.8.2, build e18a919

```

如果`docker version`、`docker info`都正常的话，可以运行一个[Nginx 服务器](https://hub.docker.com/_/nginx/)：

```
$ docker run 
-d
 -p 80:80 --name webserver nginx

```

服务运行后，可以访问[http://localhost](http://localhost/)，如果看到了 "Welcome to nginx!"，就说明 Docker for Mac 安装成功了。

![](/imgs/install-mac-example-nginx.png)

要停止 Nginx 服务器并删除执行下面的命令：

```
$ docker stop webserver
$ docker rm webserver
```



