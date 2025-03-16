
配合[[NAS里面关于docker的部署路径图]]食用


> [!note] ## Docker重要概念

![[Docker-img-240510_212446.png]]


![[Docker-img-240510_225037.png]]
### 镜像 Docker images
- 只读模板，用来创建容器
	- 它包含运行应用程序所需的文件系统和配置，比如代码、依赖、工具、库等。
- 类似java的类，可以定义属性和方法，相当于一个模板
	- docker通过模板可以创建多个容器提供相应的服务。
	- 可以类比为一个安装软件的 ISO 文件，或者是一个烤蛋糕的配方。你需要先有这个模板，才能基于它“运行”一个容器。=
- 类似于虚拟机的系统快照，是容器的“蓝图”或“基底”。
- 菜谱

### 容器 Docker containers
- 运行实例，提供独立的，可移植的环境，用于运行程序
- 类似java的实例，由类创建多个实例，实例就是类的对象
	- 容器是实际运行的应用程序实例，可以根据需求启动、停止、销毁和复制。
- 理解成简易的linux系统，docker利用容器可以独立运行一个或一组应用，容器之间相互隔离互不影响。
	- 它是一个独立运行的环境，拥有自己的文件系统、进程、网络空间，但与主机共享内核。
- 根据菜谱做的菜
	- 类比为基于一个蛋糕配方烤出来的蛋糕（镜像 → 容器）。一个镜像可以烤出多个蛋糕（多个容器），且它们互不影响。


### 仓库 Docker repository
- 用来存储镜像的地方
	- 镜像可以存储在本地仓库，也可以推送到远程仓库（如 Docker Hub）。
- 类似代码版本管理中的 Git 仓库，存储镜像的不同版本，可以方便地共享和分发。
- 仓库就像是存放蛋糕配方的“菜谱书”或“云盘”，你可以从书里翻找想要的配方（镜像）。


### 宿主机 Docker host
- Docker Host 是运行 **Docker Daemon** 的物理机或虚拟机，它是 Docker 容器实际运行的地方。
- 作用
	- 提供 Docker Daemon 所需的计算资源（如 CPU、内存、存储）。
	- 承载镜像、容器以及与 Docker 相关的文件。
- 特点
	- 可以是本地机器，也可以是远程服务器（例如云主机）。
	- Docker CLI 和 Docker Client 与 Docker Host 通信，主要通过网络（默认是 `localhost` 或 `unix://var/run/docker.sock`）。
- 本地开发时，Docker Host 就是你的开发电脑。
- 使用远程服务器时，Docker Host 是服务器（例如 AWS EC2 或其他云实例）。如阿里云服务器。


### 核心后台服务 Docker daemon
- Docker Daemon是 Docker 的核心后台服务，负责管理容器、镜像、网络和存储等资源。
- 监听 Docker CLI 的指令，执行构建、运行容器等操作。
	- 也就是一个images经过daemon运行后，就会变成一个container
- 它就像是厨房里的厨师（Daemon），负责按照配方（镜像）准备和管理蛋糕（容器）。


### 客户端 Docker client 
- 与 Docker Daemon 通信的客户端模块
- Docker Client 是 Docker 体系中的一部分，它的职责是接收用户的输入（包括通过 Docker CLI 或其他方式），并将请求发送给 Docker Daemon。
- Docker Client 不仅包括 CLI，还可以包括其他客户端接口（如 GUI 客户端或 API 客户端）。
- 它负责处理请求与 Docker Daemon 的通信，通常通过 REST API 发送指令。
- Docker CLI 是 Docker Client 的一种实现。
- Docker Client 不局限于命令行工具，它也可以是图形化工具或通过 API 与 Docker 通信的程序。


### 命令行工具 Docker CLI 
- Docker 命令行工具，用于和 Docker Daemon 交互，发送指令如 `docker run`、`docker build`。
- 类比为点菜的服务员（CLI），你通过服务员告诉厨师（Daemon）需要准备什么菜（容器 container）。
- 作用：
	- 提供一种简单的方式与 Docker 生态系统交互。
	- 将用户输入的命令转化为 **Docker API 请求**。
	- 本质是客户端的一部分，但它是特指通过终端使用的工具。

### 公共Docker镜像仓库 Docker hub
- 一个公共的 Docker 镜像仓库，可以存储和共享镜像。
- 类似于 GitHub 是代码的共享平台，Docker Hub 是镜像的共享平台。
- 类比为一个“云端菜谱书店”，你可以从中获取别人制作的配方，也可以上传自己的配方。
- 


### 相互的关系总结
- Images（镜像）**是构建和运行容器的模板。
- Container（容器）**是镜像的运行实例。
- Repository（仓库）**用于存储镜像，分为本地和远程仓库。
- Docker Daemon（守护进程）**是核心引擎，负责管理镜像和容器。
- Docker CLI**是与 Docker Daemon 交互的工具。
- Docker Hub**是一个远程仓库，用于存储和共享镜像。

### 类比一览表

| Docker 名词      | 类比              |
| -------------- | --------------- |
| Image（镜像）      | 蛋糕配方            |
| Container（容器）  | 烤出来的蛋糕          |
| Repository（仓库） | 存放配方的菜谱书        |
| Docker Daemon  | 厨师              |
| Docker CLI     | 服务员（传递指令给厨师）    |
| Docker Hub     | 云端菜谱书店（配方的共享平台） |

希望这个类比能让你对 Docker 的核心概念理解得更清楚！

### **Docker CLI + Docker Client + Docker Host 的关系**

|**概念**|**定义**|**作用**|**类比**|
|---|---|---|---|
|**Docker CLI**|Docker 的命令行工具，用户输入命令与 Docker 系统交互|转化用户指令为请求，并通过 Docker Client 发送给 Docker Daemon|服务员：收集用户点菜的指令|
|**Docker Client**|负责与 Docker Daemon 通信的模块，包含 CLI 和其他客户端工具|发送指令给 Docker Daemon，通过 REST API 或套接字通信|点餐系统：将指令发给厨师|
|**Docker Host**|运行 Docker Daemon 的机器|提供运行容器、存储镜像等计算资源，是实际执行指令的环境|厨房：烹饪的实际地方，提供设备与资源|
|**Docker Daemon**|Docker 的后台服务，运行在 Docker Host 上|实现实际的容器管理、镜像构建、网络配置等功能，执行 Docker Client 发送的命令|厨师：接收点餐系统的指令并做出菜品（容器）|、

### **工作流程示例**

假设执行命令 `docker run ubuntu`：

1. **Docker CLI**:  
    用户在终端输入命令，Docker CLI （服务员）将该命令解析为 Docker API 请求。
2. **Docker Client**:  
    Docker Client(点菜系统)（通过 CLI）将请求发送给 Docker Daemon (厨师)，通常通过套接字或网络连接。
3. **Docker Daemon（在 Docker Host 上）**:  
    Docker Daemon 接收请求，拉取 Ubuntu 镜像(菜谱)并在 Docker Host 上启动一个容器（做菜）。
4. **Docker Host**:  
    提供运行容器的物理或虚拟资源，容器最终在 Host 上运行。


---
> [!info] Docker基础命令

- **如果命令不好使，在前面加sudo

- 查找镜像:
```
docker search mysql
or
docker search mysql:8.0
```

- 拉取镜像：
```
#格式为 镜像提供方/镜像名:版本
docker pull linuxserver/mysql:latest
```

- 列出所有docker镜像：
```
docker images
```

- 删除所有镜像：
```
docker rmi -f $(docker images -q)
```

- 列出所有容器：
```
docker ps -a
```

- 列出正在运行的容器(带CPU/内存)
```
docker ps -s
```

- 暂停容器运行
```
docker pause <container>

#演示
docker pause mysql
```

- 停止所有容器
```
docker stop $(docker ps -q)
```

- 取消暂停容器运行
```
docker unpause <container>

#演示
docker unpause mysql
```

- 重启一个容器
```
docker restart <container>

#演示
docker restart mysql
```


- 停止容器运行
```
docker stop <container>

#演示
docker stop mysql
```

- 杀死一个容器
```
docker kill <container>

#演示，将指定的容器强制关闭
docker kill mysql
```

- 删除所有容器
	- 删除所有停止运行的容器
```
docker rm $(docker ps -aq) -f
```

- 显示容器的端口映射：[[Container Port 端口映射]]
	- 查看容器所使用的端口号
```
docker port <container>

#演示
docker port mysql
```

- 显示容器的控制台日志
```
docker logs <container>
#演示
docker logs mysql
```

- 阻塞容器
	- 阻塞运行直到容器停止运行，然后打印退出的代码。
```
docker wait <container>

#演示
docker wait mysql
```

- 连接到现有容器（exec）
	- 启动一个新的进程进入容器正在执行的终端交互界面
```
docker exec -it <container/id> /bin/bash

#演示
docker exec -it mysql /bin/bash
```

- 查看容器的元数据（详细信息）

```
docker inspect <container>

#演示
docker inspect mysql
```

- 获取服务器实时事件
```
docker events <container>

#演示
docker events mysql
```

- 连接到现有容器（attch）
	- 进入容器正在执行的终端交互界面，并且不会启动新的进程。
```
docker attach <container>

#演示
docker attach mysql
```

- 查看容器内部运行进程
	- 查看指定容器内部的实时进程情况
```
docker top <container>

#演示
docker top mysql
```

- 查看容器资源使用情况
	- 查看指定容器占用的服务器资源
```
docker stats <container>

#演示
docker stats mysql
```

- 列出对容器所做的更改
	- 用于比较一个 Docker容器 不同版本提交的文件差异
```
docker diff <container>

#演示
docker diff mysql
```

> [!question] Docker的部署

- 基础：创建一个新的容器并运行一个命令
	- docker最简单的方式就是docker run了。想要运行什么服务，就run相应的镜像。
	- 创建后直接进入容器交互界面，之后如果Ctrl+C退出则会连着容器一起挂起（暂停运行）。
```
docker run [OPTIONS] IMAGE [COMMAND] [ARG...] 
#演示 使用nginx:latest镜像创建并运行一个名为mynginx的容器 
docker run --name mynginx nginx:latest
```

- -d: 后台运行容器，并返回容器ID
	- 以后台模式运行容器，即在容器创建成功并启动后在后台运行，并返回容器ID信息。
```
#使用docker镜像nginx:latest以后台模式启动一个容器,并将容器命名为mynginx。

docker run -d --name mynginx nginx:latest
```

- --name: 为容器指定一个名称
	- 为创建的容器设置一个名称
	- 名称可以自己设置
	- 格式为：--name XXX
```
docker run -d --name mynginx nginx:latest

#说明
docker run：启动一个容器。
-d：后台模式运行容器
--name：设置容器名称为mynginx
nginx:latest：镜像来源：nginx:latest
```

- -i: 以交互模式运行容器
	- 创建并启动容器后自动进入容器交互页面
	- 指示docker要在容器上打开一个标准的输入接口（控制台交互界面）
	- 通常与-t同时使用
```
docker run -i nginx:latest /bin/bash

#说明：
docker run：启动一个容器。
-i：以交互模式启动（进入容器中）
nginx:latest：镜像来源：nginx:latest
/bin/bash：进入容器后要执行的命令，这里是打开终端。
root@b8573233d675:/# ：已经进入了容器里面的终端，用户名变化。
```

- -t: 以交互模式（伪终端）运行容器
	- 创建并启动容器后自动进入容器交互页面
	- 为容器重新分配一个伪输入终端（控制台交互界面），通常与 -i 同时使用。
	- 组合使用方法为-it
```
docker run -it nginx:latest /bin/bash

#说明：
docker run：启动一个容器。
-it：以交互模式启动（进入容器中）
nginx:latest：镜像来源：nginx:latest
/bin/bash：进入容器后要执行的命令，这里是打开终端。
root@b8573233d675:/# ：已经进入了容器里面的终端，用户名变化。
```


---

- @小知识
- 从本行开始
- 需要几个参数就写几个参数
- （仅限参数，如退出容器自动删除容器这中只需要一个即可。）
```
docker run -p 80:80 -p 90:90 -v /data:/data -d nginx:latest

#例如此条，有两个端口需要映射就添加两条-p端口映射参数
```

- -p: 指定端口映射
	- 将容器内部的端口映射出来，映射到宿主机上。
	- 非常常用，从容器外访问容器内服务的主要方式。
	- 映射时要保证宿主机上没有占用需要映射的端口
	- 如果占用了就自己换一个或者调整
	- 格式为：主机(宿主)端口:容器端口
	- 访问时就是宿主机IP:容器映射的端口来访问容器内部的服务
```
docker run -d --name mynginx -p 8080:80 nginx:latest

#说明：
docker run：启动一个容器。
-d：以后台模式启动。
--name mynginx：将容器命名为mynginx。
-p 8080:80：将容器的 80 端口映射到主机的 8080 端口
nginx:latest：镜像来源：nginx:latest
```

- --dns: 容器使用指定的DNS服务器IP
	- 设置容器使用指定的DNS服务器IP
	- 如果不添加此参数，那么默认的就是使用宿主机所使用的DNS
	- 格式为：--dns 8.8.8.8
```
docker run -d --name mynginx -p 8080:80 --dns 8.8.8.8 nginx:latest

#说明：
docker run：启动一个容器。
-d：以后台模式启动。
--name mynginx：将容器命名为mynginx。
-p 8080:80：将容器的 80 端口映射到主机的 8080 端口
--dns 8.8.8.8：设置容器使用指定的8.8.8.8DNS服务器IP
nginx:latest：镜像来源：nginx:latest
```

- --rm：容器退出时自动删除容器
	- 常用于临时容器，在容器退出时自动删除容器。
```
docker run -it --rm ubuntu:14.04 bash

#说明：
docker run：启动一个容器。
-it：以交互式模式运行容器，进入容器终端界面。
--rm：设置此容器退出时自动删除此容器
ubuntu:14.04：镜像来源：ubuntu:14.04
bash：交互式Shell页面
```

- -v：将主机的目录/文件挂载到容器中
	- --volume / -v: 绑定一个卷到容器中
	- 常用于容器数据持久化存储
	- 意思就是将宿主机指定的一个文件夹/文件挂载到容器内部指定的目录/文件上，这样容器内产生的数据就会存储在宿主机文件夹内，即便是容器删除了也不影响数据的留存。
```
docker run --name mynginx -p 8080:80 -v /volume1/data:/data -d nginx:latest、

#说明：
docker run：启动一个容器。
--name mynginx：将容器命名为mynginx。
-p 8080:80：将容器的 80 端口映射到主机的 8080 端口
-v /volume1/data:/data：将主机的目录 /volume1/data 映射到容器的 /data上
-d：以后台模式启动。
nginx:latest：镜像来源：nginx:latest
```

- -e：设置容器环境变量
	- 设置容器的环境变量
	- 可以自定义修改容器的环境变量参数
	- 不同的环境变量需要参考容器所需参数
```
docker run --name mysql \
  -p 3306:3306 \
  -v $HOME/mysql/conf.d:/etc/mysql/conf.d \
  -v $HOME/mysql/data:/var/lib/mysql \
  -v /etc/localtime:/etc/localtime:ro \
  -e MYSQL_ROOT_PASSWORD=123456 \
  -d mysql:5.7.23

#说明
-e MYSQL_ROOT_PASSWORD=123456 \这条参数的设置就是将MySQL数据库的密码设置为123456，此密码可以自己修改。
```

- --env-file：从指定文件读取环境变量
	- 将容器的环境变量单独写在.env文件中
	- 添加参数从指定目录内的.env文件中读取环境变量参数
	- 常用于docker-compose方式部署容器
```
docker run -tid --env PATH=/volume1/docker/mysql/bin:$PATH --rm mysql:8.0

#说明
映射目录/volume1/docker/mysql/bin内的.env配置文件到容器
```

- --link：连接到其他容器
	- 可以通过绑定所需要的容器
	- 通过容器名之间互相通信，容器间共享环境变量。
	- 主要用来解决两个容器通过IP地址连接时容器IP会变的问题
```
docker run -itd --name nginx01 --link tomcat01 nginx

#说明
以nginx镜像后台运行启动并进入交互式界面，创建nginx01容器，并与tomcat01容器连接，使其互相通信。
```

- --privileged：以特权模式运行容器
	- 以特权模式运行容器，使该容器具备访问宿主机系统的权限，等于直接操作你的宿主机系统。
	- 使用--privileged参数会照成容器逃逸
	- 意思就是有概率有人攻破你的容器，再从你的容器内攻入你的宿主机系统。
	- 企业内谨慎使用，个人你怕个蛋。
```
docker run --privileged=true -it ubuntu

#说明
赋予ubuntu容器特权模式运行
```

- --device：为容器添加指定访问权限
	- 为了系统安全，但是容器又必须使用宿主机上的设备访问权限
	- --device：此参数对容器进行授权宿主机的设备访问权限
	- 或者使用下面的参数
	- --cap-add：设置权限
	- --cap-drop：关闭权限
```
docker run --device=/dev/sda:/dev/xvdc -it ubuntu

或者

docker run --cap-add=NET_ADMIN -it ubuntu
```

- --restart：重启策略
	- 为了保证容器运行时健壮性（自愈），Docker 提供了容器重启策略，即使用参数 --restart，它可以让容器在退出时自动尝试重启。
	- no：默认策略，在容器退出时不重启容器。启动容器时不添加参数 --restart 即可。
	- on-failure：在容器非正常退出时（退出状态非0），才会重启容器。
	- on-failure:n：在容器非正常退出时重启容器，并且指定重启次数。n 为正整数。如果不指定次数，则会一直重启。例如：on-failure
	- always：容器退出时总是重启。
	- unless-stopped：在容器退出时总是重启容器，但是 Docker 守护进程启动之前就已经停止运行的容器不算在内。
```
docker container update --restart=always [容器名/容器id]

#说明
将重启策略更新到指定的容器中
```

- -c：限制容器对CPU的使用
	- -c 或 --cpu-shares
	- -c：CPU权重
	- --cpu：CPU核数
	- -cpus： 限制容器运行的核数；从docker1.13版本之后，docker提供了--cpus参数可以限定容器能使用的CPU核数。这个功能可以让我们更精确地设置容器CPU使用量，是一种更容易理解也常用的手段。
	- --cpuset-cpus： 限制容器运行在指定的CPU核心； 运行容器运行在哪个CPU核心上，例如主机有4个CPU核心，CPU核心标识为0-3，我启动一台容器，只想让这台容器运行在标识0和3的两个CPU核心上，可以使用cpuset来指定。
```
# containerA的cpu share 1024， 是containerB 的两倍。
# 当两个容器都需要CPU资源时，containerA可以得到的CPU是containerB 的两倍。
# 需要特别注意的是，这种按权重分配CPU只会发生在CPU资源紧张的情况下。
# 如果containerA处于空闲状态，这时，为了充分利用CPU资源，containerB 也可以分配到全部可用的CPU。
docker run --name "cont_A" -c 1024 ubuntu docker run --name "cont_B" -c 512 ubuntu

# 容器最多可以使用主机上两个CPU ，除此之外，还可以指定如 1.5 之类的小数。
docker run -it --rm --cpus=2 centos /bin/bash

# 表示容器中的进程可以在 CPU-1 和 CPU-3 上执行。
docker run -it --cpuset-cpus="1,3" ubuntu:14.04 /bin/bash

# 表示容器中的进程可以在 CPU-0、CPU-1 及 CPU-2 上执行。
docker run -it --cpuset-cpus="0-2" ubuntu:14.04 /bin/bash
```

- -m：限制容器对内存的使用
	- -m 或 --memory：设置内存的使用限额，例如：100MB，2GB。
	- --memory-swap：设置内存+swap的使用限额。
	- 默认情况下，上面两组参数为-1，即对容器内存和
```
# 允许该容器最多使用200MB的内存和100MB 的swap。
docker run -m 200M --memory-swap=300M ubuntu


# 容器最多使用200M的内存和200M的Swap
docker run -it -m 200M ubuntu
```

- --hostname：更改容器内的主机名
	- 在计算机中，hostname是指设备或机器的名称。在 docker 容器中，它也是一个标识符，用于标识容器。默认情况下，docker 容器的 hostname 是随机分配的，但是可以通过修改其值来自定义 hostname。
	- --hostname 标志只会更改容器内的主机名。如果你的应用程序需要主机名的特定值，则可能需要这样做。它不会更改 docker 之外的 DNS，也不会更改网络隔离，因此它不会允许其他人使用该名称连接到容器。
	- 可以使用容器名称或容器的（短，12 个字符）id 使用 docker 的嵌入式 dns 从容器连接到容器，只要您在同一网络上拥有两个容器并且该网络不是默认网桥。
```
docker run --hostname test --ip 10.1.2.3 ubuntu:14.04

#说明
创建一个 docker 容器，其基本映像为 ubuntu-14.04，主机名为 test，容器 ip 地址为 10.1.2.3
```

- --add-host：为容器增加 host 指向
	- 例如安装jellyfin影视容器，为容器增加 host 指向，加速海报与影视元数据的搜刮。
	- 相关的host可以自己搜索/测试后添加进去。
	- 一行一个host进行添加
	- host格式：网站 优选IP
```
sudo docker run -d --name=Jellyfin -p 8096:8096 \  # --name=Jellyfin 将容器名定义为 Jellyfin 
	-p 8920:8920 -p 7359:7359/udp -p 1900:1900/udp #这三个端口为可选项 \
	-v /srv/jellyfin/config:/config -v /srv/jellyfin/cache:/cache -v /media:/media \
	-e TZ=Asia/Shanghai -e PUID=0 -e PGID=0 \	#将容器的时区设为上海,使用窗口在运行时使用root权限
	--device=/dev/dri:/dev/dri \	#直通显卡给 Docker 容器，用于硬解
	--add-host=api.themoviedb.org:13.224.161.90 \	#为容器增加 host 指向，加速海报与影视元数据的搜刮
	--add-host=api.themoviedb.org:13.35.8.65 \
	--restart unless-stopped \
	jellyfin/jellyfin:latest
```


- --network：指定容器使用的网络类型
	- 指定容器的网络连接类型
	- 安装 Docker 以后，会默认创建三种网络，可以通过 docker network ls 命令查看。
	- 支持四种类型： bridge、host、none、container

- bridge：为每个容器分配、设置IP等，并将容器连接到一个docker0虚拟网桥，默认为该模式。
	- （解释：最常用的是可以手动设置容器对外的端口，比如需要访问容器内的88端口，可以将容器内部88端口映射到宿主机的任意空闲端口上。）
- host：容器不会虚拟出自己的网卡，配置自己的IP等，而是使用宿主机的IP和端口。
	- （解释：例如容器内部对外使用的88端口会自动映射到宿主机88端口上，如果宿主机88端口是被占用的，那么容器就会启动失败。）
- none：容器独有的Network namespace，但没有对其进行任何网络设置，如分配veth pair和网桥连接、IP等。
	- container：新创建的容器不会创建自己的网卡，配置自己的IP，而是和一个指定的容器共享IP、端口范围等。

- Docker创建容器模板
	- 简答创建容器
	- 模板中的参数需要多少个就加多少行对应的参数。不需要的可以删除。
	- 模板中的注释不要写进去
```
docker run -d \    #前台运行容器不输入-d，后台运行输入-d，前台交互运行-i或-it，交互后台运行-itd。
    -p 9096:8096 \    #将容器的8096端口映射到主机的9096端口上
    -p 8888:88 \    #将容器的88端口映射到主机的8888端口上
    --name=S20306 \    #自定义容器名
    -v /volume1/docker/test:/mnt/test \    #将宿主机的/volume1/docker/test目录映射到容器/mnt/test目录
    -v /volume1/docker/config:/mnt/config \    #将宿主机的/volume1/docker/config目录映射到容器/mnt/config目录
    -v /var/run/docker.sock:/var/run/docker.sock \    #允许Docker CLI与Docker Daemon进行通信，从而实现对Docker容器的管理和控制。
    -e TZ=Asia/Shanghai \    #将容器的时区设为上海
    -e PUID=0 \    #约等于指定用户权限去运行容器，root用户是0，查看当前登录用户的数值SSH内输入id即可查看。
    -e PGID=0 \    #约等于指定用户权限去运行容器，root用户是0，查看当前登录用户的数值SSH内输入id即可查看。
    --add-host=api.themoviedb.org:13.224.161.90 \    #为容器增加 host 指向，加速海报与影视元数据的搜刮。
    --add-host=api.themoviedb.org:13.35.8.65 \    #为容器增加 host 指向，加速海报与影视元数据的搜刮。
    --device=/dev/dri:/dev/dri \    #直通核显给Docker容器，用于硬件解码。
    --privileged=true \    #设置容器使用特权模式，如果选择了--device参数就不用设置此行。
    --cpus=2 \    #设置此容器最多可以使用2个CPU核心运行
    -m=2G \    #设置此容器最多可以使用2GB内存运行
    --restart unless-stopped \    #设置容器自动重启
    --network=testnetwork \    #设置容器网络为host，如果选择了上面的-p端口映射，就不需要此行。如果是指定网络就需要提前创建好网络，格式为：--network=XXX
    --link nastool \    #通过容器名之间互相通信，容器间共享环境变量。
    jellyfin/jellyfin:latest    #选择镜像来源和版本
```

- 如果是一行命令创建容器，就将\符号删除，改成一行命令即可。
```
#只是演示，根据自己的需要添加参数即可。
docker run --name reference -itd -p 9667:3000 wcjiang/reference:latest
```

- Docker进阶命令
	- 进入容器Bash交互页面
	- 例如进入jellyfin容器的bash页面
```
docker exec -it jellyfin /bin/bash

#演示，进入之后就可以执行你的后续操作
root@NAS:~# docker exec -it jellyfin /bin/bash
root@2be7994cb319:/#
```

- 宿主机与容器直接拷贝文件
	- 将jelyfin容器内根目录下的/jellyfin/wwwroot目录拷贝到主机的/volume1/docker目录下
```
#格式：docker cp 容器名或容器id:/容器内的目录或文件 宿主机存放拷贝出来的文件的目录

docker cp jellyfin:/jellyfin/wwwroot /volume1/docker
```

- 将宿主机/volume1/docker/wwwroot目录拷贝到jellyfin容器根目录下的/jellyfin目录内
```
#格式为：docker cp 宿主机需要拷贝的文件或文件夹路径 容器名或容器id:存放所拷贝文件的路径

docker cp /volume1/docker/wwwroot jellyfin:/jellyfin/
```
- 未完待续